todo: make generic? though the idea still comes from one market

# About this document

What this document is:
- a strategical suggestion
- a technical overview
- a work in progress

What this document is not:
- a legally binding document

Therefore importantly for any discussion:
- potential misinterpretation by adversaries is negligible
- implicit effects of mechanisms do not require explicit explanations, because interlocking mechanisms are created exactly to achieve a lot implicitly
- exact programmatic description of mechanisms are out of scope
- typo related comments are not welcome

---

# Rationale

Current day hiring is dominated by spam and malpractice from all participants:
- fake jobs
- fake incentives
- fake justifications
- fake workers
- fake applications
- fake experience
- fake intentions

This makes hiring market a highly adversarial environment.

Suppose what promotes spam:
- zero costs for actions or trivial costs
- zero transparency
- no requirement for any commitments
- no rewards for productive behavior

What we want to achieve ultimately is incentives for good behavior and penalties for bad behavior.

What is qualified as ideal behavior:
- posting jobs that employer actively wants to fill with real people, being as open and clear as possible
- applying to jobs that the applicant feels actually quailified for and carefully self-selects for

What is qualified as bad behavior:
- lying, misinformation, obscuring facts
- discrimination
- unsolicited data collection
- unthoughtfullness
- commitment aversion

What is important to understand is that no automation platform can realistically take on a role of truth arbiter.
So it cannot enforce good behavior or make bad behavior impossible. The only thing that can be done is to build an incentive structures
and record systems that make such decisions easier for parties on personal basis. Read on on how this outcome is intended to be achieved.

What the platform to satisfy these conditions MUST do:
- replace conventional HR systems by building a completely different incentive structure
- be an open market with clearly communicated risk structures
- make sure that costs are tied to bad behavior
- make sure that good behavior under ideal circumstance can be free or approaching free (perfect deal is possible)
- make all interactions as public as legally possible unless it directly opposes the incentive goals
- keep all data immutable
- introduce mandatory floor costs equalizable per praty type
- be clear about what can be known and what can only be assumed
- have cost structure sufficient for platform continuation
- if legally pressured to change anything anywhere, make sure to keep area of damage contained, designated, recorded and broadcast
- make sure that ALL important decisions are decided BY the parties on THEIR discretion using THEIR stakes

What the platform to satisfy these conditions MUST NOT do:
- replace conventional HR systems by incorporating their qualities
- have any logic that explicitly diverges based on its lifetime
- introduce decision biases of its own in any way
- model the expected economy of hiring
- become arbiter of truth
- be protector of bad financial decisions for any parties
- allow amending records
- promote risky behavior
- arbitrarily change cost structures
- assign any credibility to anything but the facts recorded in the ledger and presence of history
- assume that there exists or should be achieved some form of perfect equilibrium, convergence, mass or information density
- try to account in any way for anything happenning out of band, including but not limited to:
  - assume any credibility for any out of band data

---

# Proposed protocol roughly

- Both employers and employees need to make stakes on matching.
- Stakes may be of uneven ratio e.g. 10:1.
- Employers can post a vacancy and "invest" a stake volume for it.
- Employers can set a minimum applicant stake e.g. at $10.
- Employers can set a stake growth logic and factors:
  - linear growth with min growth = min stake
  - geometric growth with min factor = 1.05
  - exponential growth with min factor = 1.05
- Employer sees only one applicant at a time in the queue based on FIFO logic.
- Employees expend stake on rejection at a certain rate, e.g. 1:1 to the stake size.
- Employers expend stake if there are applicants in queue, each N unit of time, equal to the highest queue stake.
- Employer is free to terminate the vacancy whenever the applicant queue is empty.
- When vacancy terminates any remaining employee stake is returned to their balance.
- If vacancy stake is spent, vacancy is terminated in a day if not invested in further.
- All vacancies ever published are always publicly visisble.
- All employer decisions or non-decisions per vacancy are a fully public record at all times.
- Employer can choose an application as a match, terminating the vacancy. This is free.
- On rejection Employer can choose to ban the applicant from further applications to them.
- All bans given by the employer are fully public.
- Employer can choose to revert a ban by paying the initial rejection ban stake again.
- Employer can set a maximum concurrent outgoing applications limit as a pre-apply filter, as well as total bans filter.
- Employer can change their mind about any of the previous inbound applications overriding them as a match, paying the initial stake for it again, paying current queue max stake as indecision fee, and paying a stake for any top queue application. Previous decisions records are kept immutable, override is recorded as another extra decision on top.
- Vacancy is immutable employer during its lifetime.
- Applicants make a stake to apply.
- Applicants loose the stake if rejected.
- Double apply to the same vacancy is impossible.
- The stakes are rising with each applicant currently in vacancy queue. Minimum stake reduces to the original value only if the queue gets emptied.
- If an applicant is chosen as a match their stake is returned.
- Each rejection becomes public on the active vacancy immediately.
- When vacancy terminates all remaining queue stakes are returned to the applicant balances.
- For all applicants, details of current outgoing applications on active vacancies are hidden from everyone except one at a time to the vacancy owner.
- Statistic on current outgoing applications of all applicants are always public.
- After vacncy termination all actions of all applicants about it become fully public.
- All bans received by the applicant are fully public.
- Expended stakes are paid toward the platform.
- All data committed to the platform requires explicit public domain commitment by the EULA.
- If any data is mandated to be removed by effective legal framework, deletions must be targeted, visible, or at least the fact that deletions took place must be fully recorded and public.
- Platform allows fully public discussion under any currently visible item: Employer, vacancy, recorded stall, reinvest, applicant, application, rejection, match, ban, deletion record etc.

---

# Inner workings

## Terminology

### Owner

Multiple entities, records, processes can have an owner entity. Typically owner is the one who was responsible for the related item to appear.
Term Owner can be used to refer to that entity in context to make sure its role is clear relative to the class of such entities.

### Reputation, Rep

Reputation is the assumption of trustworthiness towards entities on the platform.
Platform NEVER computes, derives, suggest reputation in any form.
Platform NEVER assigns or imports such from anywhere else as well.
Reputation assumption is an intangible personal decision of each individual active party about other parties.

Things that can be trusted ensured by platform mechanisms:
- all related records eventually become public, mostly instantly;
- all related records are kept immutable on best effort basis unless law is involved;
- if law is involved, the maximally transparent record of law based decisions is kept;
- that financial spending decisions of the parties on the platform are visible;
- that any signalled intentions of the parties are backed by staked money;
- that platform never arbiters what decisions can be made or should be made, simply free of bias;

Examples of things that cannot be trusted:
- that any of the parties are who they assume themselves to be;
- that any signalled intentions of the parties are true;
- that matching has actually resulted in a hire;
- that rejections actually resulted in no hires;

## Automation mechanisms

### Employer

Ties togeter:
- a balance account
- vacancies
- vacancy decisions
- list of bans

- Employers can freely create vacancies with desired settings given sufficient balance for the initial investment.
- Employers can freely terminate vacancies if they have an empty queue.

TBD

### Applicant

Ties togeter:
- a balance account
- applications

TBD

### Balance account

Balance is an internal ledger of funds injected into the platform and spent on it.
Platform transactions only operate over internal balances of the parties.
This ensures stakes can be committal.
Protects from certain fraud types.
All employers and applicants have their own balances.
Balance is NOT public because it signals no intent, but if public can be used to target abuse.

### Vacancy

todo:
- vacancy with balance and empty queue can be kept indefinitely - PROBLEM, needs solution (easy exploit via unrealistic stake)

TBD

Potential adversarial vectors:
- vacancy with balance and empty queue can be in theory kept indefinitely with unrealistic stake
  - potential goals:
    - advertisement, publicity
  - counters:
    - it is publicly visible that an unrealistic vacancy is held indefinitely, potentially tainting the rep
    - specific audience means that said publicity is likely to be negative or advertisement ineffective
    - a counter-adrversary may choose to actually stake in, wasting adversary money

### Vacancy queue

todo:
- queue size is unbounded by necessity
- total queue stake can be higher than current vacancy balance by necessity, or else adversarial info is exposed
- queue can never result in locking

TBD

### Application

Is an item in Vacancy queue.

TBD

### Inbound application

This simply means current top application in FIFO vacancy queue from the perspective of vacancy owner.
Besides application owner, only vacancy owner can see all information about it.
For other parties this application is obscured with only statistical information given until it is processed further.

### Stall

As invariant is considered existing for each complete unit of "Stall duration" since the moment vacancy queue has an available applicant
to the moment the decision on that application is made. The actual data record is created at earlies techonolgically possible opportunity.

todo:
- note stall is unbounded by necessity

TBD

### Rejection

Employer has to pay a stake 

TBD

### Ban

Ban associates a pair Employer-applicant and a stake at the time of ban.
When active relationship is present applicant may not apply to vacancies of this employer.
Employer can terminate ban by paying an associated stake.

This way indecisiveness is paid for twice.

### Match

A match is a terminal signal event for the related vacancy and does not imply, enforce, or verify employment.

TBD

### Reversion

When created, ties together multiple entities:
- vacancy
- a match
- current inbound application

Reversion allows to rever a prior rejection decision for any of priorly rejected application in the vacancy.

Since it creates a match, it also terminates the vacancy.

Reversion decision can be made if there is enough balance on the vacancyt to:
- pay reversion fee for the Match decision, which is free under normal flow, but here either the top queue stake or the stake at the time of prior rejection has to be paid
- pay regular rejection stake to sanction rejection decision for the current inbound application if any; this rejection does not have a ban attachment option
- pay unban fee if prior rejection was also tied to a ban decision

Further penalty sturctures for reversion should not be out of the picture.

TBD

### Discussion point

Each entity in the list is automatically considered a discussion point:
- Employer
- Applicant
- Vacancy
- Application
- Rejection
- Ban
- Match
- Reversion
- Stall

Discussion points allow for free public immutable discussions.
Discussions are not staked.
This exists as convenience layer. Keep in mind that since platform is public, discussion can be out of band anyway, so any protocol here is less important.
Therefore the exact mechanisms are out of scope for this doc at this time.

### Legal change point

Legal change point can be attached to any aforementioned item if any change to them is enforced by effective law that the project has to follow. Typically this means law depending on geography of hosting.
Legal change point highlights what kind of infromation was changed or removed, from where, based on what decision, based on what request, how it was received, and who was responsible for compliance enactment.
Legal change points are also immutable and public, with the same law related exceptions pertaining (which means legal point may cascade into further points).

Project is obliged to make sure redactions are kept minimally required. Cryptographic chain functions may be used in all entities to ensure history compromise is visible.

Project is obliged to make sure that invoking law for redactions has detrimental effects on rep to make it the least attractive option.
E.g. all entities have a visible counter of how many legal change points are related to them with links.
At this point it will affect reputations of owners in a way that is potentially less preferable to owning mistakes.

# Attack surfaces

todo: Can an employer cycle reinvestments to farm applicant stake burn? - technically impossible, no incentive, public rep
todo: Can applicants grief employers by inflating queue stake growth without intent to match? - technically possible, bounded, no incentive, public rep, explicitly accepted risk, opt in
todo: Predatory configurations that exist only to burn applicant stake. - technically possible, bounded, no incentive, public rep, explicitly accepted risk, opt in

TBD

# TODOs

todo: explain why platform lifetime has zero bearing on outcomes, as necessitated by ensured mechanisms and what can and cannot be "trustworthy"

TBD



