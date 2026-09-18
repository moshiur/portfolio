# Guest self-check-in kiosk and back-office

**2026 · hospitality client · web kiosk, guest registration, provider integration, ops tooling**

Guests arriving at a hospitality property check themselves in at an unattended kiosk in the
entrance, or from their own phone before arrival. The system collects what the law requires
for guest registration, files it with the national tourism registration provider, and gives
the staff a back office to see and fix what came in.

Two hard parts: the kiosk has to keep working with nobody watching it, and the registration
data has to be *legally* right, not just present.

## The kiosk has no operator

An unattended terminal cannot be left to a browser tab that quietly stopped. The kiosk
reloads itself on a schedule so a stale page can never greet a guest, and a watchdog
restarts the session when the device wakes up wrong. Card-reader failures on site are part
of the job: several trips were about a chip reader that behaved differently from the one on
the desk.

Guest-facing flows are a wizard: arrival, personal details, co-travellers, signature, done.
Every field that the registration authority rejects has to be caught *before* the guest
walks away, because a correction afterwards means chasing someone who has already left.

## Registration data has to be legally correct

Guest registration (Meldeblatt) is a legal document, which makes ordinary web-form thinking
insufficient:

- **Co-travellers** are people, not a headcount. Adding one late, from the back office,
  has to produce the same filing as one entered at the kiosk.
- **Birth year and document issuing country** are mandatory for some guests and not others,
  and the rules differ by nationality.
- **Arrival and departure dates** change after the fact — early departures, extended stays —
  and each change is a correction to a filing that already exists, not a fresh one.

Each of these arrived as a production defect or an authority rejection, and each was fixed
in the model rather than patched in the form.

## When the integration is the one that's wrong

The clearest example: registrations began failing with a provider error code that pointed at
our payload. Reading the logs against the data showed our records were complete, and the
failures correlated with guests whose details had been added through the **provider's own
web client** rather than ours — a path we did not control and had not been told about.

That took reproducing the case, comparing both data paths, and taking it to the provider with
evidence rather than a complaint. They confirmed it, and the corrections went out across
several releases while the property kept checking guests in.

The lesson worth keeping: when a third-party integration fails, the first job is to prove
which side is wrong, with data, before either side starts guessing.

## The back office is the actual product

Reception staff spend more time in the operations views than guests spend at the kiosk:
search across guests and registration sheets, disposition of who is where, guest cards, and
export into the property-management system. Most of the small, unglamorous work — list
scrolling that survives a long season, a search that finds a name typed three ways, a spam
hint on the contact form — came from watching the staff use it.

Alongside the features: releases roughly every few days, production deployments, an AWS bill
trimmed by removing infrastructure nobody was using, and integration secrets moved into
managed parameter storage instead of configuration files.

**Skills:** web kiosk UX for unattended terminals, regulated data modelling, third-party API
integration and incident diagnosis, back-office tooling, AWS operations and cost control,
frequent release cadence with production support.
