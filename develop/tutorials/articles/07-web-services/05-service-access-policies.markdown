# Service Access Policies

Service Access Policies are an additional layer of web service security, 
defining services or service methods that can be invoked remotely. For more 
detail, and information on managing Service Access Policies, see 
[the user guide article on Service Access Policies](/discover/deployment/-/knowledge_base/7-0/service-access-policies). 

There may be cases, however, where your app needs to integrate with a Liferay 
instance's Service Access Policies. This kind of integration can be done on two 
levels. 
<!-- What are some use cases where someone may want to do this? -->
<!-- What's the other level, besides portal? -->

On the portal level, the 
[package `com.liferay.portal.kernel.security.service.access.policy`](https://docs.liferay.com/portal/7.0/javadocs/portal-kernel/com/liferay/portal/kernel/security/service/access/policy/package-summary.html) 
provides classes for basic access to policies. For example, you can use the 
[singleton `ServiceAccessPolicyManagerUtil`](https://docs.liferay.com/portal/7.0/javadocs/portal-kernel/com/liferay/portal/kernel/security/service/access/policy/ServiceAccessPolicyManagerUtil.html) 
to obtain Service Access Policies configured in the system. You can also use the 
[`ServiceAccessPolicyThreadLocal` class](https://docs.liferay.com/portal/7.0/javadocs/portal-kernel/com/liferay/portal/kernel/security/service/access/policy/ServiceAccessPolicyThreadLocal.html) 
to set and obtain Service Access Policies granted to current request thread. 
<!-- What is accessing/setting policies used for? -->

Furthermore, Liferay's Service Access Policy API and implementation is provided 
via the following OSGi modules:

- `com.liferay.service.access.policy.api.jar`
- `com.liferay.service.access.policy.service.jar`
- `com.liferay.service.access.policy.web.jar`

These OSGi modules can be used to manage service access policies 
programmatically.
<!-- 
How? 
What is meant by "manage service access policies automatically"? 
-->

A custom token verification module: 
<!-- What's a custom token verification module, and how does it fit in with this tutorial? -->

- should use `ServiceAccessPolicyThreadLocal#addActiveServiceAccessPolicyName()` 
  to grant the associated policy during web service request.

- can use `com.liferay.service.access.policy.api.jar` and  
  `com.liferay.service.access.policy.service.jar` to create policies 
  programmatically

- can use `ServiceAccessPolicyManagerUtil` to display list of supported policies 
  when authorizing remote application to associate token with an existing 
  policy. 
