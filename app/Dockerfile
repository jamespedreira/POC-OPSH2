FROM microsoft/dotnet:2.2-aspnetcore-runtime AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM microsoft/dotnet:2.2-sdk AS build
WORKDIR /src
COPY ["Token/Token.csproj", "Token/"]
RUN dotnet restore "Token/Token.csproj"
COPY . .
WORKDIR "/src/Token"
RUN dotnet build "Token.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Token.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Token.dll"]