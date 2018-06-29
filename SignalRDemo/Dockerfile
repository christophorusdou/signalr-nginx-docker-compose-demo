FROM microsoft/dotnet:2.1-aspnetcore-runtime AS base
WORKDIR /app
ENV ASPNETCORE_URLS http://+:5000
EXPOSE 5000

FROM microsoft/dotnet:2.1-sdk AS build
WORKDIR /src
COPY SignalRDemo/SignalRDemo.csproj SignalRDemo/
RUN dotnet restore SignalRDemo/SignalRDemo.csproj
COPY . .
WORKDIR /src/SignalRDemo
RUN dotnet build SignalRDemo.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish SignalRDemo.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SignalRDemo.dll"]
