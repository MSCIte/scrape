# scrape
🤨🤨🤨

COHERE PROMPT (it's kinda large tho)
```
Given a list of course requirements strings,  extract the requirements to JSON.

It should follow the format of:
[id: string]: {
  "prereqs": [string[]],
  "coreqs": [string[]],
  "antireqs": [string[]],
  "instructorPermission": boolean,
  "requiredMajor": string | null,
  "requiredTerm": "string | null,
  "otherNotes": string
}

1A, 1B, 2A, 2B, etc. are different school terms.
Slashes between course codes mean OR. For example, "PHYS 123/453" means "PHYS 123" OR "PHYS 453".

Overall example:
###
INPUT: {
  1: "Prereq: Level at least 4A Architecture.  Cumulative Major Average at least 73%; Coreq: ARCH 492"
  2: "CHE Grad Students Only - all others require permission of department."
  3: "Pre/Co-req: ECE 650 or 750 Tpc 26, or instructor consent. Antireq: ECE 355, ECE 451, CS 445, CS 645, SE 463, ECE 452, CS 446, CS 646, SE 464"
  4: "Prereq: Arts and Business students. Antireq: AFM 101, 102, BUS 127W/227W, 247W, MSCI 262"
  5: "Prereq: (One of MATH 106, 114, 115, 136, 146, NE 112) and (One of MATH 128, 138, 148). Antireq: AMATH 251, 350, MATH 218, 228"
}
### 
OUTPUT: {
  1: {
    "prereqs": [],
    "coreqs": [
      "ARCH 492"
    ],
    "antireqs": [],
    "instructorPermission": false,
    "requiredMajor": null,
    "minimumTerm": "4A",
    "otherNotes": "Cumulative Major Average at least 73%"
  },
  2: {
    "prereqs": [],
    "coreqs": [],
    "antireqs": [
    ],
    "instructorPermission": false,
    "requiredMajor": "CHE Grad",
    "minimumTerm": null,
    "otherNotes": ""
  },
  3: {
    "prereqs": {
      "type": "OR",
      "data": [
        "ECE 650",
        "ECE 750"
      ]
    },
    "coreqs": [],
    "antireqs": [
      "ECE 355",
      "ECE 451",
      "CS 445",
      "CS 645",
      "SE 463",
      "ECE 452",
      "CS 446",
      "CS 646"
    ],
    "instructorPermission": true,
    "requiredMajor": "CHE Grad",
    "minimumTerm": null,
    "otherNotes": ""
  },
  4: {
    "prereqs": [],
    "coreqs": [],
    "antireqs": [
      "AFM 101",
      "AFM 102",
      "BUS 127W",
      "BUS 227W",
      "BUS 247W",
      "MSCI 262"
    ],
    "instructorPermission": false,
    "requiredMajor": "Arts and Business",
    "minimumTerm": null,
    "otherNotes": ""
  },
  5: {
    "prereqs": {
      "type": "AND",
      "data": [
        {
          "type": "OR",
          "data": [
            "MATH 106",
            "MATH 114",
            "MATH 115",
            "MATH 136",
            "MATH 146",
            "NE 112"
          ]
        },
        {
          "type": "OR",
          "data": [
            "MATH 128",
            "MATH 138",
            "MATH 148"
          ]
        }
      ]
    },
    "coreqs": [],
    "antireqs": [
      "AMATH 251",
      "AMATH 350",
      "MATH 218",
      "MATH 228"
    ],
    "instructorPermission": false,
    "requiredMajor": "Arts and Business",
    "minimumTerm": null,
    "otherNotes": ""
  }
}
###
INPUT: {
1: "Prereq: MATH 237 or 247. Antireq: PHYS 365",
2: "Prereq: (AMATH 242/CS 371 or CS 370) and STAT 231/241",
3: "Prereq: Level at least 3A Honours Anthropology",
4: "Prereq: BIOL 308 or 309; CHEM 233 or 237; (BIOL 308 or BIOL 309) and co-req CHEM 233 or CHEM 237 for Science and Business/Biotechnology Specialization or Honours Biotechnology/Economics or CS Honours Bioinformatics",
5: "Prereq: BIOL 361; Not open to students in the Faculty of Mathematics.  Antireq: (for Arts and Environmental Studies students) PSYCH 202, 391, STAT 322, 430",
###
OUTPUT: 

```
