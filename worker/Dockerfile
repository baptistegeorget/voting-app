FROM mcr.microsoft.com/dotnet/sdk:7.0
WORKDIR /service/worker
COPY . .
RUN dotnet restore
RUN dotnet publish -c release --self-contained false --no-restore
CMD [ "dotnet", "bin/release/net7.0/Worker.dll" ]