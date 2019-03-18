---
layout: default
title: Terminology
permalink: /docs/terminology/
---

### [specification]({{site.baseurl}}/docs/specification/)
A description of the interface between an application and a test definition. Specifies the expectation of the test and the ways the test buckets map to application-level properties. Consists of *tests*, *buckets*, and *context*. Used to generate the interface code.

### [test-matrix]({{site.baseurl}}/docs/matrix-schema/)
A list of active *test definitions* used by all applications compiled into a single file. Generated by the *builder* and loaded by each application.

### <a name="context"></a>context
A collection of application-specific variables available in the test definition rules. In a web application, these variables typically map directly to the properties of a request, such as `logged-in`, `country`, `language` and `user-agent`.

### test ( _experiment_ )
A set of behaviors simultaneously delivered to different users to assess effects on user actions.

### test definition
A description of the ways users are assigned to buckets in the test. Specifies the active buckets, eligibility rules, allocation rules, test group sizes, test constants, and the salt.

### group ( _bucket_ )
A single behavior within a test. A group, also called a bucket, is determined by evaluating a test definition in the test matrix using the provided identifier and context. Each bucket has a name, integer value, and optional payload containing test-specific data.

### payload
Optional data associated with each test bucket that defines one aspect of the bucket's behavior.

### <a name="eligibility-rule"></a>eligibility rule
An expression determining whether a test-definition is relevant for a provided context. If this expression evaluates to `false`, no bucket for this test should be selected.

### allocation
A description of the test's group sizes (bucket distribution). A test-definition can have multiple allocations that are conditionally used depending on its *allocation rule*.

### <a name="allocation-rule"></a>allocation rule
An expression determining whether an allocation is relevant for a provided context. If an allocation's expression evaluates to `true`, its group sizes should be used.

### <a name="identifier"></a>identifier
An id that will be used when determining the active groups. The id is typically unique and persistent across requests (session cookie, account id, etc). Each identifier is associated with a specific test-type. The groups are determined by evaluating the test-matrix for a specified identifier and context.

### test-type
An enumeration of the identifier to use when allocating test buckets:

- `USER`: A unique value identifying a user; typically a tracking cookie value
- `ACCOUNT`: An account-based identifier, fixed across devices; typically a user-id
- `EMAIL`: An email address of a user
- `RANDOM`: No identifier is used

### <a name="test-constants"></a>test constants
Variables you can reference in an *eligibility rule* or *allocation rule*.

### <a name="special-constants"></a>special-constants (test-definition)
-- NOTE: interaction between special-constants + rule containing "${}" braces. (convertToConsumableTestDefinition)

### [builder]({{site.baseurl}}/docs/builder)
A tool responsible for generating the test-matrix your applications consume. The tool validates test-definitions, which are stored across multiple files, and combines them into a single file.

### user
A client consuming your service. Your A/B tests should be designed to influence the behavior of an individual directly (changing a UI element/funnel) or indirectly (changing the algorithm used to display search results). Your application should record and measure user behavior so your A/B tests can be evaluated.

For most web applications, a user represents a human using your application. In some circumstances, a user could represent another application consuming your service, such as another application consuming the application's API.