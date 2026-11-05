# Harborline Platform Operations Handbook

> Maintained by the Platform Reliability Guild. This handbook records how Harborline's
> shared platform services are owned, released, and reviewed.

## Service ownership

| Service | Owning team | Primary on-call | Escalation channel |
| --- | --- | --- | --- |
| ledger-api | Payments Core | payments-oncall | #payments-incidents |
| control-plane | Tenancy Platform | tenancy-oncall | #tenancy-incidents |
| ingest-gateway | Data Ingestion | ingest-oncall | #ingest-incidents |
| risk-engine | Risk & Underwriting | risk-oncall | #risk-incidents |
| notifications | Tenant Experience | notify-oncall | #notify-incidents |
| platform-jobs | Platform Reliability | platform-oncall | #platform-incidents |

Changes to ownership require a two-approver review from the Platform Reliability Guild.

## Open remediation backlog

- [ ] **ledger-api/src/reconcile/refund_replay.ts:412** - Add an idempotency guard when replaying refund batches (ref: #2)
- [ ] **ledger-api/src/payouts/fx_quote_cache.ts:96** - Cache FX quotes for repeated corridor lookups (ref: #4)
- [ ] **ledger-api/src/webhooks/signature_verify.ts:57** - Rotate webhook signing keys without dropping in-flight deliveries (ref: #5)
- [ ] **control-plane/src/audit/retention_policy.py:77** - Apply the 400-day retention policy to audit tables (ref: #8)
- [ ] **console/src/features/disputes/DisputeTimeline.tsx:142** - Show dispute evidence upload progress (ref: #10)
- [ ] **ingest-gateway/src/parsers/csv_stream.py:63** - Stream CSV imports instead of buffering whole files (ref: #12)
- [ ] **ingest-gateway/src/validators/schema_drift.py:149** - Detect schema drift before batch commit (ref: #14)
- [ ] **risk-engine/src/scoring/rules_engine.py:322** - Version rule packs independently of the service (ref: #15)
- [ ] **risk-engine/src/scoring/rules_engine.py:408** - Add shadow scoring for new rule packs (ref: #16)
- [ ] **notifications/src/channels/sms_fallback.py:204** - Fall back to SMS when email delivery fails (ref: #19)
- [ ] **notifications/src/templates/localisation.py:91** - Localise notification templates for new markets (ref: #20)
- [ ] **platform-jobs/src/scheduler/retry_policy.ts:238** - Apply jittered exponential backoff to job retries (ref: #22)


Shared platform services ship on a two-week train. Code freeze is Tuesday 18:00 UTC of
the second week; production rollout starts Wednesday 09:00 UTC after the change advisory
review. Emergency patches need an incident ticket and a rollback plan.

## Incident review process

Every Sev-1 and Sev-2 incident gets a blameless review within five business days. The
review owner files follow-up issues and links them from the incident record. Recurring
themes are raised at the monthly reliability forum.

## Appendix: escalation contacts

- Payments Core duty manager: payments-dm@harborline.example
- Tenancy Platform duty manager: tenancy-dm@harborline.example
- Platform Reliability duty manager: platform-dm@harborline.example
