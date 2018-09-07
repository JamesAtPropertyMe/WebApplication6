FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 8080/tcp

#FROM microsoft/dotnet:2.1-sdk AS build
#WORKDIR /src
#COPY ["WebApplication6/WebApplication6.csproj", "WebApplication6/"]
#RUN dotnet restore "WebApplication6/WebApplication6.csproj"
#COPY . .
#WORKDIR "/src/WebApplication6"
#RUN dotnet build "WebApplication6.csproj" -c Release -o /app
#
#FROM build AS publish
#RUN dotnet publish "WebApplication6.csproj" -c Release -o /app
#
#FROM base AS final
#WORKDIR /app
#COPY --from=publish /app .
#ENTRYPOINT ["dotnet", "WebApplication6.dll"]

FROM microsoft/dotnet:sdk AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM microsoft/dotnet:aspnetcore-runtime
WORKDIR /app
COPY --from=build-env /app/out .
EXPOSE 8080/tcp
ENTRYPOINT ["dotnet", "WebApplication6.dll"]