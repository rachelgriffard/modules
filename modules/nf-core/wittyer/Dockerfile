# syntax=docker/dockerfile:1-labs
FROM mcr.microsoft.com/dotnet/sdk:10.0@sha256:ea13841f10c6c410a6df63c6c97ab549dfd2b5fcfff1c00186531ba30208117d as builder

ADD https://github.com/Illumina/witty.er.git#v0.5.2 /src

WORKDIR /src/Wittyer
RUN dotnet publish -f net6.0 -r linux-x64 -c Release -o /output \
    && chmod +x /output/Wittyer

FROM mcr.microsoft.com/dotnet/runtime:10.0@sha256:b1fc29ba8c7cf56eacc4aaf078dbbfa70b533130968957356d0fef95d3ac62ac

LABEL git_repository=https://git.illumina.com/DASTE/Ilmn.Das.App.Wittyer.git
WORKDIR /opt/Wittyer
RUN apt-get -y update && apt-get -y install tabix libunwind8 openssl procps
COPY --from=builder /output /opt/Wittyer
