FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.2-stretch AS build
WORKDIR /src
COPY ["MicroRabbit.Catering.Api/MicroRabbit.Catering.Api.csproj", "MicroRabbit.Catering.Api/"]
COPY ["MicroRabbit.Infra.Ioc/MicroRabbit.Infra.Ioc.csproj", "MicroRabbit.Infra.Ioc/"]
COPY ["MicroRabbit.Cataring.Data/MicroRabbit.Cataring.Data.csproj", "MicroRabbit.Cataring.Data/"]
COPY ["MicroRabbit.Cataring.Domain/MicroRabbit.Cataring.Domain.csproj", "MicroRabbit.Cataring.Domain/"]
COPY ["MicroRabbit.Domain.Core/MicroRabbit.Domain.Core.csproj", "MicroRabbit.Domain.Core/"]
COPY ["MicroRabbit.Catering.Application/MicroRabbit.Cataring.Application.csproj", "MicroRabbit.Catering.Application/"]
COPY ["MicroRabbit.Infra.Bus/MicroRabbit.Infra.Bus.csproj", "MicroRabbit.Infra.Bus/"]
RUN dotnet restore "MicroRabbit.Catering.Api/MicroRabbit.Catering.Api.csproj"
COPY . .
WORKDIR "/src/MicroRabbit.Catering.Api"
RUN dotnet build "MicroRabbit.Catering.Api.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "MicroRabbit.Catering.Api.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "MicroRabbit.Catering.Api.dll"]