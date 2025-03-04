{% include quickstart-intro.md %}

- The syntax used to describe the interactions is described [here](general-guidance.html#search-syntax).
- See the [General Guidance] section for additional rules and expectations when a server requires status parameters.
- See the [General Guidance] section for additional guidance on searching for multiple patients.

#### Mandatory Search Parameters:

The following search parameters and search parameter combinations SHALL be supported:

1. **SHALL** support searching for all conditions including problems, health concerns, and encounter diagnosis for a patient using the **[`patient`](SearchParameter-us-core-condition-patient.html)** search parameter:

    `GET [base]/Condition?patient={Type/}[id]`

    Example:
    
      1. GET [base]/Condition?patient=1137192

    *Implementation Notes:* Fetches a bundle of all Condition resources for the specified patient ([how to search by reference])


#### Optional Search Parameters:

The following search parameter combinations SHOULD be supported:

1. **SHOULD** support searching using the combination of the **[`patient`](SearchParameter-us-core-condition-patient.html)** and **[`clinical-status`](SearchParameter-us-core-condition-clinical-status.html)** search parameters:

    `GET [base]/Condition?patient={Type/}[id]&clinical-status=http://terminology.hl7.org/CodeSystem/condition-clinical|active,http://terminology.hl7.org/CodeSystem/condition-clinical|recurrance,http://terminology.hl7.org/CodeSystem/condition-clinical|remission`

    Example:
    
      1. GET [base/Condition?patient=1032702&amp;clinical-status=http://terminology.hl7.org/CodeSystem/condition-clinical\|active,http://terminology.hl7.org/CodeSystem/condition-clinical\|recurrance,http://terminology.hl7.org/CodeSystem/condition-clinical\|remission

    *Implementation Notes:* Fetches a bundle of all Condition resources for the specified patient and all &#34;active&#34; statuses (active,relapse,remission). This will not return any &#34;entered in error&#34; resources because of the conditional presence of the clinicalStatus element. ([how to search by reference] and [how to search by token])

1. **SHOULD** support searching using the combination of the **[`patient`](SearchParameter-us-core-condition-patient.html)** and **[`category`](SearchParameter-us-core-condition-category.html)** search parameters:

    `GET [base]/Condition?patient={Type/}[id]&category={system|}[code]`

    Example:
    
      1. GET [base]/Condition?patient=1032702&amp;category=http://terminology.hl7.org/CodeSystem/condition-category\|problem-list-item
      1. GET [base]/Condition?patient=1032702&amp;category=http://hl7.org/fhir/us/core/CodeSystem/condition-category\|health-concern
      1. GET [base]/Condition?patient=1032702&amp;category=http://terminology.hl7.org/CodeSystem/condition-category\|encounter-diagnosis

    *Implementation Notes:* Fetches a bundle of all Condition resources for the specified patient and category. ([how to search by reference] and [how to search by token])

1. **SHOULD** support searching using the combination of the **[`patient`](SearchParameter-us-core-condition-patient.html)** and **[`code`](SearchParameter-us-core-condition-code.html)** search parameters:

    `GET [base]/Condition?patient={Type/}[id]&code={system|}[code]`

    Example:
    
      1. GET [base]/Condition?patient=1032702&amp;code=[http://snomed.info/sct\|442311008]

    *Implementation Notes:* Fetches a bundle of all Condition resources for the specified patient and code. ([how to search by reference] and [how to search by token])

1. **SHOULD** support searching using the combination of the **[`patient`](SearchParameter-us-core-condition-patient.html)** and **[`onset-date`](SearchParameter-us-core-condition-onset-date.html)** search parameters:
    - including support for these `onset-date` comparators: `gt,lt,ge,le`
    - including optional support for composite *AND* search on `onset-date` (e.g.`onset-date=[date]&onset-date=[date]]&...`)

    `GET [base]/Condition?patient={Type/}[id]&onset-date={gt|lt|ge|le}[date]{&onset-date={gt|lt|ge|le}[date]&...}`

    Example:
    
      1. GET [base]Condition?patient=555580&amp;onset-date=ge2018-01-14

    *Implementation Notes:* Fetches a bundle of all Condition resources for the specified patient and date.  ([how to search by reference] and [how to search by date])



{% include link-list.md %}
