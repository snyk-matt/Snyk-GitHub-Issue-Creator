# Snyk GitHub Issue Creator

The GitHub Issue creator utilizes Snyk's API to create a GitHub Issue for vulnerabilities or license issues you may have in your projects in Snyk. It's currently set up to run as a GitHub action executing on a cron job daily at midnight. However, with GitHub Actions, this can be triggered with a pull request, commit, etc. Since it utilizes [Snyk's API](https://snyk.docs.apiary.io/#introduction), there's plenty of customization for what type of issues you'd like to add to GH. 

Once an issue has been fixed in Snyk, the issue in GitHub will be closed the next time the program is run. Currently, it's set up to add vulnerabilities that are fixable, and that have not yet been fixed in Snyk.

References to Snyk's API and some example configurations utilizing its [Reporting API](https://snyk.docs.apiary.io/#reference/reporting-api/latest-issues/get-list-of-issues) (using the section titled `Get list of issues`) shown below:

## Template for preffered attributes and filters:

```json
{
  "filters": {
    "orgs": [],
    "severity": [
      "high",
      "medium",
      "low"
    ],
    "exploitMaturity": [
      "mature",
      "proof-of-concept",
      "no-known-exploit",
      "no-data"
    ],
    "types": [
      "vuln",
      "license"
    ],
    "languages": [
      "javascript",
      "ruby",
      "java",
      "scala",
      "python",
      "golang",
      "php",
      "dotnet",
      "swift",
      "docker"
    ],
    "projects": [],
    "issues": [],
    "identifier": "",
    "ignored": false,
    "patched": false,
    "fixable": false,
    "isFixed": false,
    "isUpgradable": false,
    "isPatchable": false,
    "isPinnable": false
  }
}
```

## Reference for the filters shown above:

- `orgs` (***required***): 
  - `array`
  - The list of orgIds (or single orgId) to filter results by. This is the orgId found in Snyk.

- `severity`: 
  - `array` 
  - The severity levels of issues to filter by:
    - `high`: `string` - Include issues with high severity.
    - `medium`: `string` - Include issues with medium severity.
    - `low`: `string` - Include issues with low severity.

- `exploitMaturity`: 
  - `array` 
  - The exploit maturity levels of issues to filter the results by:
    - `mature`: 
      - `string`
      - Include issues which a published code exploit can easily be used for.
    - `proof-of-concept`:
      - `string`
      - Include issues for which a published, theoretical proof-of-concept or detailed explanation that demonstrates how to exploit this vulnerability is available.
    - `no-known-exploit`:
      - `string`
      - Include issues for which neither a proof-of-concept code nor an exploit were found for.

- `types`:
  - `array`
  - The type of issues to filter the results by.
  
- `languages`:
  - `javascript`:
    - `string`
    - Include issues which are for JavaScript projects (npm or yarn package managers).
  - `ruby`:
    - `string`
    - Include issues which are for Ruby projects (rubygems package manager).
  - `java`:
    - `string`
    - Include issues which are for Java projects (maven or gradle).
  - `scala`:
    - `string`
    - Include issues which are for Scala projects (sbt).
  - `python`:
    - `string`
    - Include issues which are for Python projects (pip).
  - `golang`:
    - `string`
    - Include issues which are for Golang projects (golang, golangdep, govendor or gomodules).
  - `php`:
    - `string`
    - Include issues which are for PHP projects (composer).
  - `dotnet`:
    - `string`
    - Include issues which are for .Net projects (nuget, paket).
  - `swift` or `objective-c`:
    - `string`
    - Include issues which are for Swift/Cocoapods projects (cocoapods).
  - `docker`:
    - `string`
    - Include issues which are for docker projects (apk, deb, rpm).

- `projects`:
  - `array`
  - The list of project IDs to filter issues by.

- `issues`:
  - `array`
  - The list of issue IDs to filter issues by.

- `identifier`:
  - `string`
  - Search term to filter issue name by, or an exact CVE or CWE.

- `ignored`:
  - `boolean`
  - If set to `true`, only include issues which are ignored. 
  - If set to `false`, only include issues which are not ignored.

- `patched`:
  - `boolean`
  - If set to `true`, only include issues which are patched. 
  - If set to `false`, only include issues which are not patched.

- `fixable`:
  - `boolean`
  - If set to `true`, only include issues which are fixable.
  - If set to `false`, only include issues which are not fixable.

- `isFixed`:
  - `boolean`
  - If set to `true`, only include issues which are fixed. 
  - If set to `false`, only include issues which are not fixed.

- `isUpgradable`:
  - `boolean`
  - If set to `true`, only include issues which are upgradable. 
  - If set to `false`, only include issues which are not upgradable

- `isPatchable`:
  - `boolean`
  - If set to true, only include issues which are patchable. 
  - If set to false, only include issues which are not patchable

- `isPinnable`:
  - `boolean`
  - If set to true, only include issues which are pinnable. 
  - If set to false, only include issues which are not pinnable.


### Current Configuration - Add a GitHub Issue for every *fixable* vulnerability and has *not yet been fixed*, in a *specific* organization, for *projects that are written in javascript*:

```json
{
  "filters": {
    "orgs": ["Your Snyk orgId"], 
    "severity": [
      "high",
      "medium",
      "low"
    ],
    "exploitMaturity": [
      "mature",
      "proof-of-concept",
      "no-known-exploit",
      "no-data"
    ],
    "types": [
      "vuln",
      "license"
    ],
    "languages": [
      "javascript"
    ],
    "projects": [],
    "issues": [],
    "identifier": "",
    "fixable": true,
    "isFixed": false
  }
}
```


