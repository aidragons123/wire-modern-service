# wire-modern-service

The new wire payment service. A workflow of named steps with statuses and an audit trail, ISO 20022 pacs.008 output, a fraud hold that pauses and resumes from the fraud step. This `main` branch still has two known gaps: fee rounding (HALF_EVEN) and the same-day value date.

* Source: `src/` (plain Java, no build tool needed; `javac` compiles it)
* Main class: `com.bank.wire.modern.Main`
* Java level: 18 (also compiles on 17)
* Protocol: reads one JSON payment per line on stdin and writes one JSON answer per line on stdout, in the same order.
  This is the entry point the comparison agents (Replay Agent, Live Agent) run.

Try it:

```
javac -d out $(find src -name '*.java')
echo '{"requestId":"A1","debtorName":"X","debtorAccount":"123456789","creditorName":"Y","creditorAccount":"987654321","creditorBic":"DEUTDEFF","amount":"100.00","currency":"USD","valueDate":"2030-01-04","processingDate":"2030-01-02"}' | java -cp out com.bank.wire.modern.Main
```
