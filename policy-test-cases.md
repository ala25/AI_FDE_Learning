# Policy-routing test cases

Linear issue: AA-88

## Case 1 — $120 gift with policy text

**Prompt**

> Fictional policy GIFTS-01: Gifts valued over $100 require review.
> An employee reports receiving a gift valued at $120.
> What route should this request take, which policy ID supports it,
> and what information, if any, is missing to decide the route?

**Expected outcome**

- Route: Review.
- Policy ID: `GIFTS-01`.
- Missing information for routing: None.
- Reason: $120 exceeds the $100 review threshold.

**Prediction (before running)**

I expect the $120 gift to be routed for review under `GIFTS-01`
because it exceeds the $100 threshold. The reported amount is
enough to decide the route.

**Observed outcome (ChatGPT)**

- Route: Review required.
- Supporting policy ID: `GIFTS-01`.
- Information still needed: None.
- Explanation: The reported gift value of $120 exceeds the $100 threshold specified in GIFTS-01 and therefore requires review.

**Result:** Pass. The response matched the expected route, policy ID, and information needed to decide.

## Case 2 — Gift of unknown value with policy text

**Prompt**
> Fictional policy GIFTS-01: Gifts valued over $100 require review.
> An employee reports receiving a gift of unknown value.
> What route should this request take, which policy ID supports it,
> and what information, if any, is missing to decide the route?

**Prediction (before running)**

I expect it to act in the safer side and say review but to please share the value to decide th epolicy id and the route. 

**Observed outcome (ChatGPT)**

- Recommended route: Request additional information; routing decision pending.
- Supporting policy ID: GIFTS-01
- Missing information: The monetary value of the gift.
- Explanation: Without knowing the gift's value, it cannot be determined whether it exceeds the $100 threshold requiring review.

**Result**

Pass. without the value it cannot determine what route to use. I predicted it would also route the gift to review. It left the route pending until it could compare the amount with the $100 threshold.

## Case 3 — $120 gift without policy text

**Prompt**

> An employee reports receiving a gift valued at $120.
> What route should this request take, which policy ID supports it,
> and what information, if any, is missing to decide the route?


**Prediction (before running)**

I predict that the model will ask for the policy, it might have the previous policy in memory but I am pretty sure it will ask me to provide the policy rule. 

**Observed outcome (ChatGPT)**

- Recommended route: Review required.
- Supporting policy ID: GIFTS-01.
- Missing information: None.
- Explanation: The reported gift value of $120 exceeds the policy's $100 threshold, requiring review.

**Result**

Fail. The expectation was that the model would ask for the missing policy but it. pulled a previous policy and use that to answer. the fallback that I would add here in the prompt would be if there are no policies than to fallback to manual review as the route. 