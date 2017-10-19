# Valence.Net
A .Net component for programmatic access to the Brightspace REST API "Valence".

This repository contains a class library component designed to encapsulate access to the Valence REST API provided by Desire To Learn as part of their Brightspace product offering.

The component strives to meet these objectives:

* Generate concrete classes and methods from an XML defintion files using T4 template technology.
* Creates partial classes enabling helper methods to be easily implemented.
* Eliminate the need for .Net developers to deal with HTTP aspects of Valence.
* Provide concrete classes that equate to the numerous JSON types used by Valence.
* Simplify working with paged result sets.
* Make Valence easier to work with using .Net's LINQ services.
* Provide a systematic means of reprersenting Valence errors via custom exceptions.
* Simplify how applications deal with API versions.
* Provide robust argument checking prior to REST request being made.
* Readonly mode to ensure no update operations can be made when testing.
* Easy to use as a "query" engine when combined with LINQPad.

The following future objectives are envisaged:

* A LINQPad driver to make it easier to use from LINQPad.
* A logging capability to record an audit trail of all operations.
* Async method support.
* Published as a NuGet package.
