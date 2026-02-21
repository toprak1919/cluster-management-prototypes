# Data Reference for Prototype Pages
Use this to align all prototype content with the real cluster-management codebase.

## Navigation Sidebar Structure
- **Search** (Advanced search)
- **Persons** (top-level)
  - Employees
  - Cluster members
  - BIGSAS members
  - Fellows
  - Guests
  - Similar names
  - Compare with website
- **Projects** (top-level)
  - Research sections
- **Publications** (ROLE_CORE only)
- **Events**
- **Countries**
- **Locations**
- **Institutions**
  - ACC
- **Filtered Views**
- **Feedback** (admin only)
- **Administration** (admin only)
  - Emails
  - Settings
  - Expert Sync

## Person Fields (in show page order)
1. Email(s) — multiple, each with remark
2. Homepage(s) — URL + title, multiple
3. ORCID(s) — multiple
4. Phone(s) — phone + type (mobile/work/home/fax/other), multiple
5. Gender — female/male/diverse
6. Languages spoken and written — multiple entries
7. Geographic fields of expertise — multiple
8. Thematic fields of expertise — multiple
9. Field of study — multiple
10. BIGSAS — boolean
11. Cluster — boolean
12. Entitled to vote — boolean
13. Signed Rights and Duties — boolean
14. Membership category — free text
15. Membership Start — date
16. Membership End — date
17. Position — free text
18. Location — relation
19. Managed projects — list
20. Involved projects — list with position
21. Institutions — list with role/department
22. Research Sections — list
23. Remark — text
Then sections: Addresses, Events (as host), Events (as guest), Fellowships (as fellow), Fellowships (as host), Expert Search settings, Files

## Person Listing Default Columns
Title | Last Name | First Name | Middle Name | Pseudonym | Gender | BIGSAS | Location | Languages | Thematic Fields | Geographic Fields

## Project Fields
- Title (text, required)
- Project ID (short identifier)
- Research sections (multiple)
- Institutions (multiple)
- Countries (multiple)
- Directors (persons with position: "Project Director" / "Former Project Director" / "Former Project Member")
- Duration (calculated from start/end)
- Start date
- End date
- Report deadline
- Report requested (boolean)
- Report requested on (date)
- Report submitted (boolean)
- Funding: Requested (float €) and Approved (float €)
- Gender in research question (boolean)
- Targets (according to the proposal) — text
- Expected outcome — text
- Additional information — text
- Itinerary/Activities (year + description entries)
- Workshops (linked)
- Publications (year + planned + achieved + costs)
- Involved persons (with counts: total, from UBT, from ACC, female quota, foreign female, cooperation partners)
- Tags
- Files

## Publication Fields (NOT like a journal citation!)
- Year
- Planned (text description)
- Achieved (text description)
- Costs (float)
Publications are linked to Projects, not standalone bibliographic entries.

## Event Fields
- Title
- Type of event (free text, e.g. "Conference", "Workshop")
- Applying body
- Start datetime
- End datetime
- Online? (boolean)
- Hybrid? (boolean)
- Links to online resources (text, one per line)
- Report available? (boolean)
- Hosts (persons, ManyToMany)
- Guests (PersonEvent entries with: role, purpose of stay, invited by, begin/end of stay, invited/confirmed/attended booleans)
- Locations (multiple)
- Countries (multiple)
- Tags
- Notes (text entries on the event)
- Files

## Institution Fields (very simple)
- Name
- ACC (boolean — is an African Cluster Center)
- Location (relation to Location entity)
- Linked persons (via PersonInstitution with role + department)
- Linked projects

## Fellowship Fields (simple)
- Start date
- End date
- Fellow (Person)
- Host (Person)
- Created date
NO type, NO name, NO status field.

## Research Section Fields
- Name (unique, admin-entered)
- Display order
- Spokesperson (Person)
- Linked projects
- Active people

## Location Fields
- Name
- Region
- Country (relation)
- Continent

## Approval Status
- Name (free text label for project approval states)

## Key Labels (English translations)
- "Persons" not "People"
- "BIGSAS" not "BIGSAS Member"
- "Cluster" for cluster member boolean
- "entitled to vote" (lowercase)
- "Signed Rights and Duties" (not "R&D Agreement")
- "Membership category" (not "Category")
- "Directors" for project PIs (not "PI" or "Principal Investigator")
- "Membership Start" / "Membership End"
- "Report deadline" / "Report requested" / "Report submitted"
- "Requested" / "Approved" for funding amounts
- "Expert Search" section for consent/visibility settings
- "Highest academic degree"
- "Applying body" (event organizer)
- "ACC" for African Cluster Center institutions
