# Realize multi-tenancy

Based on the [official document](https://docs.abp.io/zh-Hans/abp/latest/Multi-Tenancy) multi-tenant tutorial, add some problems and specific steps that may be encountered in actual operation:

1、Tenant login:

Based on the identityserver4 authorization center implemented by abp, the current tenant id must be specified when multi-tenant login, so that the current tenant id is included in the token.

> Add the request header to the login interface: __tenant: "tenant id"



2、Realize multi-tenancy

Generally speaking, directly enable multi-tenancy:

>  `MultiTenancyConsts.IsEnabla = true`

but when you are a multi-database multi-tenant, you need to configure tenant storage, otherwise it will throw *`not found tenant store`* exception.

**Specific steps:**

- Domain layer

    Refer to the nuget package: `Volo.Abp.TenantManagement.Domain` and depend on the `AbpTenantManagementDomainModule` module

- domain.shared layer

    Reference the nuget package `Volo.Abp.TenantManagement.Domain.Shared`; depends on the `AbpTenantManagementDomainSharedModule` module;

- entityframework layer

    Refer to the nuget package: `Volo.Abp.TenantManagement.EntityFrameworkCore`, which depends on the `AbpTenantManagementEntityFrameworkCoreModule` module;

- The dbcontext connection string must be the same as the name stored in the database, that is, the name stored in the AbpTenantConnectionStrings table is consistent with the ConnectionStringName noted by dbcontext






