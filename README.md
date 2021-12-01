# Education Crowdfunding

![Donors Choose Example](https://github.com/dssg/MLinPractice/blob/main/img/dc_img.png)

## The Organization
[DonorsChoose](https://www.donorschoose.org/) is an online crowdfunding platform that seeks to fill funding gaps faced by disadvantaged schools in the United States. On the site, teachers can post projects asking for funds to help them purchase specific resources for their classrooms (e.g. books, technology, or other supplies) and the community can make pledges to support the project. Like other crowdfunding sites, projects have a specific funding goal and are only funded at all if they reach or pass this goal. To date, the site has facilitated more than $970 million in donations to projects affecting 40 million students in the United States.


## The Problem
Although the website has successfully facilitated funding for many teachers and projects, rougly one third of the projects that are posted on the site fail to meet their funding goals, affecting students at some of the nation's most disadvantaged scools.


## Goals and Interventions
DonorsChoose would like to increase the fraction of projects that are funded on their platform, and one hypothesis about why some projects go unfunded is that the posting or requested resources might not be well-optimized to appeal to donors. As such, they have enlisted a team of digital content experts to help review and provide tailored feedback to posted projects. Unfortunately, this is manual, resource-intensive process, so they can only provide this assistance to 10% of the projects posted in a given month and therefore want to focus on projects that are unlikely to be fully funded without their intervention.


## The Data
For this project, you have access to data from DonorsChoose about projects, teachers, schools, and donations (note: DonorsChoose made this [dataset publicly available](https://www.kaggle.com/c/kdd-cup-2014-predicting-excitement-at-donors-choose) for the 2014 KDD Cup). In the database, you'll find five tables (note that you can also download the raw data in CSV format directly [here](https://dsapp-public-data-migrated.s3.us-west-2.amazonaws.com/donors_choose_2014_raw_CSVs.zip)):

- `projects` contains basic information about all the projects posted on the site, including characteristics of the teacher who posted (e.g., name, subject area, grade level, whether they participate in Teach for America, etc) it and their school (e.g., location, charter status, poverty level, NCES ID, etc).

- `essays` contains the title, short description, and full essay that is posted with project to provide potential donors with information about what the teacher is asking for and what they plan to do with the resources, how it will benefit students, etc.

- `resources` contains information about the specific resources being requested for the project (e.g., books, technology, etc), including their costs, quantities, and types.

- `outcomes` contains various calculated fields that DonorsChoose uses to characterize projects, including whether the project has received donations from other teachers, whether the project received large donations, how many donors post original messages, as well as an overall flag for "exciting" projects (see notes below)

- `donations` contains transaction-level information about the donations to each project (e.g., amount, how it came in, etc), as well as some characteristics of the donor (e.g., whether the donor is a teacher, their location, whether they left a message, etc)

A very rough data dictionary of the specific fields in each table is provided below:

### Data Fields

Table Name: *donations*
  - donationid - id of the donation given.
  - projectid - id of the project (project received the donation)
  - donor_acctid - unique donor identifier (donor that made a donation)
  - donor_city - city of the donor
  - donor_state - state of the donor
  - donor_zip - zipcode of the donor
  - is_teacher_acct - donor is also a teacher
  - donation_timestamp - the time of donation
  - donation_to_project - amount given to the project, excluding tip
  - donation_optional_support - amount of optional support
  - donation_total - total donated amount
  - dollar_amount - total amount in US dollars.
  - donation_included_optional_support - where optional support (tip) was included for DonorsChoose.org
  - payment_method - where credit card was used
  - payment_included_acct_credit - whether a portion of a donation used account credits redemption
  - payment_included_campaign_gift_card - whether a portion of a donation included corporate sponsored giftcard
  - payment_included_web_purchased_gift_card - whether a portion of a donation included citizen purchased giftcard (ex: friend buy a giftcard for you)
  - payment_was_promo_matched - whether a donation was matched 1-1 with corporate funds
  - via_giving_page - donation given via a giving / campaign page (example: Mustaches for Kids)
  - for_honoree - donation made for an honoree
  - donation_message - donation comment/message. Used to calculate great_chat
 
Table Name: *essays*
  - projectid - id of the project
  - teacher_acctid - unique teacher identifier (teacher that made the project)
  - title - title of the project
  - short_description -  a short description of the project
  - need_statement - need statement of a project
  - essay - complete project essay

Table Name: *resources*
  - resourceid - unique resource id
  - projectid - unique project id
  - vendorid - unique vendor id
  - vendor_name - name of the vendor
  - project_resource_type - Type of project resources
  - item_name - name of the resource
  - item_number - resource term identifier
  - item_unit_price - unit price of the resource
  - item_quantity - the number of items required

Table Name: *outcomes*
  - projectid - unique id of the project
  - is_exciting - whether DonorsChoose labeled the project as "exciting" (see below)
  - at_least_1_teacher_referred_donor - whether the project had at least one donor.
  - fully_funded - whether the project was fully funded or not
  - at_least_1_green_donation - the project had at least one donation or not?
  - great_chat - higher than average percentage of donors leaving an original message.
  - three_or_more_non_teacher_referred_donors - the project had three or more non teacher referred donors
  - one_non_teacher_referred_donor_giving_100_plus - the project had at least one non teacher-referred donor that gave 100 plus
  - donation_from_thoughtful_donor - project received donation from a "thoughtful" donor.
  - great_messages_proportion - proportion of great messages on the project
  - non_teacher_referred_count - count of donors that teacher did not refer

Table Name: *projects*
  - projectid - unique id of the project
  - teacher_acctid - unique teacher id
  - schoolid - unique school id of the project
  - school_ncesid - school NCES id
  - school_latitude - latitude of school's location
  - school_longitude - longitude of school's location
  - school_city - city of the school
  - school_state - state of the school
  - school_zip - zipcode of the school
  - school_metro - urban/rural area
  - school_district
  - school_county
  - school_charter - Does school belong to charter school?
  - teacher_prefix - prefix for teacher
  - teacher_teach_for_america - Does teacher teaches for america?
  - teacher_ny_teaching_fellow - Is Teacher NY teaching fellow?
  - primary_focus_subject - Primary focus of the teacher's subject.
  - primary_focus_area - Primary focus area of the teacher
  - secondary_focus_subject - Secondary focus of the teacher's subject.
  - secondary_focus_area - Secondary focus area of the teacher
  - resource_type - type of items needed
  - poverty_level - Level of poverty of the school/teacher
  - grade_level
  - fulfillment_labor_materials
  - total_price_excluding_optional_support
  - total_price_excluding_optional_support
  - students_reached
  - eligible_double_your_impact_match
  - eligible_almost_home_match
  - date_posted - Date where project was posted

**What are "exciting" projects?**
Exciting projects meet a number of requirements specified by the website.
The term is more of a business-facing term rather than implying that these projects are better or more relevant.
The criteria for an exciting project are as follows:

  1. Was the project fully funded (fully_funded) ?
  1. The project had at least one teacher-acquired donor (at_least_1_teacher_referred_donor)
  1. Has a higher than average percentage of donors leaving an original message (great_chat) ?
  1. Has at least one "green" donation (at_least_1_green_donation)?
  1. Has one or more of:
    - donations from three or more non teacher-acquired donors (three_or_more_non_teacher_referred_donors)
    - one non teacher-acquired donor gave more than $100 (one_non_teacher_referred_donor_giving_100_plus)
    - the project received a donation from a "thoughtful donor" (donation_from_thoughtful_donor)

A project should meet all of these criteria to be exciting.

This information can be found in outcomes table, including the variable *is_exciting.*

