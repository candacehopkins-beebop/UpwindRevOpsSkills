# AI security questionnaire: approved answers

Owner: Stacey (Legal)
Last reviewed: 2026-09-01
Review cadence: quarterly, or whenever hosting, model providers, or
subprocessors change

Replace `{{CUSTOMER}}` with the account name before sending. Do not edit
the wording otherwise.

---

## Does Upwind use AI-related tools?

Yes. Upwind uses artificial intelligence and machine-learning
technologies within certain Platform capabilities to assist with security
analysis, threat detection, investigation, prioritization, and generation
of security insights and recommendations. Certain features may also use
generative AI and foundation models to process information for inference.

---

## Can you provide insights on the tool/model, use cases, and benefits to your customers for using this AI service?

Upwind uses a combination of AI/ML capabilities and large language models,
including models available through enterprise cloud AI services.
AI-supported capabilities are used to analyze security telemetry and
findings, assist with threat and vulnerability investigation, contextualize
security risks, summarize findings, and generate recommendations or
responses to authorized user queries. The primary customer benefit is
helping security teams more quickly understand and prioritize security
information, investigate potential risks, and reduce the manual effort
required to interpret complex cloud and runtime security data. AI
functionality is designed to augment security teams rather than replace
human security decision-making.

---

## Where is the Upwind service that uses AI hosted?

Upwind's Platform, including the environment supporting its AI-enabled
capabilities for {{CUSTOMER}}, is hosted in the United States on AWS.
Certain AI-enabled functionality may use approved third-party AI/model
providers for inference. These providers are subject to Upwind's
applicable security, privacy, and data-protection requirements.

---

## Where will our data be stored, and would using the service involve any cross-border data transfers?

{{CUSTOMER}}'s data will be hosted and stored in the United States within
Upwind's U.S.-based cloud environment. AI-enabled services applicable to
{{CUSTOMER}} are also configured to support processing within the United
States. Accordingly, use of the service is not expected to require
cross-border transfers of {{CUSTOMER}} data outside the United States as
part of normal service delivery.

---

## Will our confidential, proprietary, or private information be used as input to this service? Would it be used to train the models?

Upwind's AI-enabled functionality is intended to process security-related
information necessary to provide the applicable Platform capabilities.
Depending on the feature being used, this may include customer security
telemetry, findings, metadata, or information submitted by an authorized
user. Upwind does not use {{CUSTOMER}} Customer Data to train or fine-tune
third-party foundation models, nor does Upwind permit its AI service
providers to use Customer Data to train their models. AI processing is
performed for purposes of providing the applicable service or inference
functionality. Customers should not intentionally submit unnecessary
confidential information or personal information through free-form AI
inputs.

---

## Are there plans to mitigate the inherent issues of GenAI, such as hallucinations? For example, a manual validation step for critical decisions.

Yes. Upwind treats generative-AI output as assistive rather than
authoritative. AI-generated summaries, explanations, recommendations, and
similar outputs are intended to help users investigate and understand
security information and do not replace appropriate human judgment for
material security decisions. Customers retain the ability to review the
underlying security context and determine the appropriate action. Upwind
does not rely solely on generative-AI output to autonomously make critical
customer security decisions. Human review and validation remain
appropriate before taking consequential actions based on AI-generated
recommendations.
