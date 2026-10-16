# Warehouse final project

Work on application classes in `src/` and test drivers in `tests/`.
The Stage 1 foundation was copied from
PreviousAssignments/Project1Stage1Group-main/WarehouseStage1.
The original Stage 1 files and LibraryFinal sample remain as references.

## Layout

```text
src/                  Application Java source
tests/                Java test drivers
bin/                  Generated .class files (ignored by Git)
requirements/         Final assignment document and project checklist
PreviousAssignments/  Earlier assignments and original Stage 1 source
LibraryFinal/         Instructor's reference implementation
.tools/               Portable JDK (local, ignored by Git)
.vscode/              VS Code configuration
```

## Compile and run

With a JDK on PATH, run these commands from the project root:

```powershell
javac -d bin src\*.java
java -cp bin UserInterface
```

Compile and run the test drivers separately:

```powershell
javac -cp bin -d bin tests\*.java
java -cp bin ClientTest
java -cp bin ProductTest
java -cp bin WishlistItemTest
java -cp bin StoreSystemTest
java -cp bin PaymentTest
```

For a demonstration using the assignment's exact commands, run them inside
`src/`. This puts generated class files beside the source; they are ignored by Git:

```powershell
cd src
javac *.java
java UserInterface
```

## Java and VS Code setup

A portable JDK used for verification is available locally in .tools/jdk
(ignored by Git). This workspace's .vscode/settings.json configures it for
Java projects and adds JAVA_HOME and the JDK bin folder to new VS Code terminals.
Install Microsoft's Extension Pack for Java from the Extensions view, reload
the window, and open a fresh terminal. Run java -version and javac -version
to confirm that both are available. No system-wide Java installation is needed.

The local VS Code settings are ignored by Git because the runtime entry has
an absolute path. If you move the project, update java.configuration.runtimes
in .vscode/settings.json to the new JDK location. The Windows terminal paths
use workspaceFolder and follow the project automatically.

For a PowerShell terminal outside VS Code, use this session-only setup first:
  $jdk = (Get-ChildItem .tools/jdk -Directory | Select-Object -First 1).FullName
  $env:Path = "$jdk\bin;$env:Path"

VS Code uses `src` and `tests` as source folders and `bin` as its output folder.
After a layout change, run Developer: Reload Window from the Command Palette
if VS Code still shows old source locations.

## Implemented features

The current program supports creating clients/products, adding or replacing
wishlist quantities, recording payments, and displaying clients, products,
wishlists, individual client details and transaction histories.
Use numeric IDs (1, 2, 3); C1/P1 in the assignment are example names.
StoreSystem remains the single coordinator, keeping the Stage 1 structure.
Small integration changes validate model data, protect collection membership,
and handle invalid console input and end-of-input cleanly.

Payment menu options:

- **8:** Receive a client payment.
- **9:** Display a client's details and balance.
- **10:** Display a client's transactions.

Payments follow PreviousAssignments/ReceivePaymentFromAClient.pdf:
find the client, show the current balance, request a positive amount, credit
the account and show the updated balance. Invalid amounts are requested again;
an unknown client ends the operation without any changes. Payments are recorded
independently of ordering and shipping; the program does not transfer funds.
A negative account balance is displayed as an absolute credit amount.

All monetary APIs now use BigDecimal. Construct amounts from strings, e.g.
new BigDecimal("100.00"). Amounts must be positive and exactly representable
in whole cents; fractional cents are rejected rather than silently rounded.
Transactions store a date, description and signed amount: charges are positive,
payments are negative. Client.debit is available for later fulfillment charges;
checkout and shipment processing will call it when invoices are implemented.

`PaymentTest` verifies the previous assignment's $200 balance examples:

- $100 payment -> $100 owed.
- $200 payment -> $0 balance.
- $300 payment -> $100 credit.

It also checks prepayments, invalid requests, exact cent arithmetic, transaction
history, and preservation of other clients, inventory and wishlist data.
The test seeds charges directly; the current UI only supports payments.

Checkout, product waitlists, invoices and save/load are still to be implemented.
Data currently lasts only for the running session.
See requirements/project-checklist.md for the full 150-point scope.

Compile only `src/` and `tests/`, not all folders recursively: the references
contain duplicate class names, including UserInterface.
