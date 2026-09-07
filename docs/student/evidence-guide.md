# Task 1.2 evidence guide

Use [the frozen evidence pack](evidence-pack.json) for every graded answer. Run the
local scenario as required practical investigation and retain that evidence for
the final engineering defense. Local timings and generated IDs will differ; do
not substitute them for the supplied pack in `submission.yaml`.

The pack records real synthetic requests against an isolated Compose stack. Its
provenance distinguishes captured HTTP, Redis, logs, Jaeger and Prometheus output
from exact source excerpts. The capture uses Task 1.3's opening runtime, which
retains Task 1.2's business behavior and telemetry defects; its additional empty
transport carrier field does not repair propagation. No hosted model or cloud
measurement is represented.

1. Read `HTTP`, then correlate the exception ID through `QUEUE`, `WORKER`,
   `MODEL`, `STATE` and `API-TRACE`. The boundary fields select the primary record
   category for each boundary: HTTP response, stream entry, worker log/span,
   model span, and saved status record, respectively. `sample-only` is a fictional
   shape example, never evidence for this Task.
2. Map A-G to the scenario's seven operations: sending the alert, validating and
   persisting queued work, publishing, returning the HTTP response, consuming,
   calling the model and saving the summary. Give immediate causal predecessors,
   not every earlier step. Background scheduling can overlap the HTTP response;
   timestamp order alone does not establish a required predecessor.
3. In Jaeger, `traceID` identifies a trace and `spanID` identifies one operation.
   A `CHILD_OF` reference names its parent. Shared exception IDs establish a
   correlation even when traces are disconnected. Nearby timestamps alone do not.
4. Jaeger `duration` values are microseconds: divide by 1,000,000 for seconds.
   Subtract the saved record's `accepted_at` from `updated_at` for the persistence
   interval. Round the three numeric answers to three decimals; their absolute
   tolerance is 0.001 seconds. These intervals overlap and must not be added.
5. Read metric sample names, application labels, bucket bounds and source
   observation conversion together. A metric name ending in `_seconds` does not
   prove that its input was converted correctly. A configured provider delay is
   not an observed runtime duration.
6. Classify each exact claim in the pack: `observation` is directly present in a
   record or source excerpt, `inference` is a causal explanation drawn from that
   evidence, and `not-established` needs evidence that this pack does not supply.

The schema and comments provide the complete choices. Empty fields parse as YAML
but fail completeness; the sample demonstrates shape and deliberately fails
protected correctness. Source excerpts and traces are investigation inputs, not
a completed answer sheet. Repair no source code in this Task.
