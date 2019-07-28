##Advance Application Input Configuration

###Introduction

The Django portal for Apache Airavata middleware is new and caters to wider range of requirements from Gateways. <br>
    
One major requirement was more flexibility in application inputs. In the previous PGA, inputs were Integer, String, Number and URI. 
User requirements were to have more options when adding these input types to their applications, such as option buttons, Cascading inputs, etc…

In  Django in order to advance the input types JSON scripting is used. 
When using JSON scripting, prior the developer/gateway admin need to add the component in to Django framework in order for it to work.

###String Input Validations

