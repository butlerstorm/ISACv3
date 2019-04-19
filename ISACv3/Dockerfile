#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see http://aka.ms/containercompat 

FROM microsoft/dotnet:2.2-runtime-nanoserver-1803 AS base
WORKDIR /app

FROM microsoft/dotnet:2.2-sdk-nanoserver-1803 AS build
WORKDIR /src
COPY ISACv3/ISACv3.csproj ISACv3/
RUN dotnet restore ISACv3/ISACv3.csproj
COPY . .
WORKDIR /src/ISACv3
RUN dotnet build ISACv3.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish ISACv3.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ISACv3.dll"]
