# Analysis — platform overview

Heavy Rental is a capital-intensive equipment hire product split across four product repos and three supporting repos. The documentation pack must present one architecture without duplicating every source-repo spec file.

**Strategic constraints**

- Vocareum/Academy IAM cannot create roles (`LabRole` only).
- Local development uses three Compose packs, not a monorepo.
- AI work must not corrupt OLTP (pull-merge, skip on primary down).
- Submission requires UML in Mermaid and PlantUML.

**Implications**

- Spring is the public façade; Haystack is an internal capability plane.
- Specs in this pack are documentation-grade as-built contracts, linked to upstream `openspec/` where it exists.
