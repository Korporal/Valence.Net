# Valence.Net
A .Net component for programmatic access to the Brightspace REST API "Valence".

This repository contains a class library component designed to encapsulate access to the Valence REST API provided by Desire To Learn as part of their Brightspace product offering.

The component strives to meet these objectives:

* Generate concrete classes and methods from an XML defintion files using T4 template technology.
* Creates partial classes enabling helper methods to be easily implemented.
* Eliminate the need for .Net developers to deal with HTTP aspects of Valence.
* Provide concrete classes that equate to the numerous JSON types used by Valence (over 100 classes)
* Simplify working with paged result sets.
* Make Valence easier to work with using .Net's LINQ services.
* Provide a systematic means of representing Valence errors via custom exceptions.
* Simplify how applications deal with API versions.
* Provide robust argument checking prior to REST request being made.
* Readonly mode to ensure no update operations can be made when testing.
* Easy to use as a "query" engine when combined with LINQPad.

The following future objectives are envisaged:

* A LINQPad driver to make it easier to use from LINQPad.
* A logging capability to record an audit trail of all operations.
* Async method support.
* Published as a NuGet package.

Here's an example of how we define an endpoint method in the XML file used by the T4 processor:

    <MethodClass Name="Grades">

        <Method Path="/d2l/api/le/(version)/(orgUnitId)/grades/values/(userId)/"
          Action="GET"
          Name="GetAllGradesForUser"
          Comment="Get all of the grade values for a student in an org unit.">
        <Parameters>
          <Parameter Name="version" Type="D2LVERSION"/>
          <Parameter Name="orgUnitId" Type="D2LID"/>
          <Parameter Name="userId" Type="D2LID"/>
        </Parameters>
        <Return Type="List[Grade.ComputableGradeValue]"/>
      </Method>

    </MethodClass>

This generates a method with this signature:

    public List<Grade.ComputableGradeValue> GetAllGradesForUser (string version, string orgUnitId, string userId) 

Which is accessed at runtime like this:

    var grades = session.Grades.GetAllGradesForUser("latest","1234","0123"); // use the latest version 
    
The grades result is a list of ComputableGrade objects:

    namespace Valence.Grade
    {
        /// <summary>
        /// The framework can provide grade values slightly differently depending upon whether the underlying grade object type is a computable value, or not (basically, only Text (4) grade types are not computable).
        /// </summary>
        public class ComputableGradeValue 
        {
            // SEE: http://docs.valence.desire2learn.com/res/grade.html#Grade.GradeValue
            public string UserId { get;  set; }
            public string OrgUnitId { get;  set; }
            public string DisplayedGrade { get;  set; }
            /// <summary>
            /// Unique global ID, can be used when updating a grade.
            /// </summary>
            public string GradeObjectIdentifier { get;  set; }
            public string GradeObjectName { get;  set; }
            public GRADEOBJ_T GradeObjectType { get;  set; }
            public string GradeObjectTypeName { get;  set; }
            public RichText Comments { get;  set; }
            public RichText PrivateComments { get;  set; }
            public double? PointsNumerator { get; set; }
            public double? PointsDenominator { get;  set; }
            public double? WeightedDenominator { get;  set; }
            public double? WeightedNumerator { get;  set; }
        }
    }

