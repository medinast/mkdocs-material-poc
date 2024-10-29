# Loan Modifications

## Overview

Lenders of loans serviced on Nelnet Velocity may offer some type of loan modifications in their Loan Program to assist customers who are having difficulty making payments.

Qualification requirements vary by lender and loan program.

Processors have the ability to edit certain loan modifications directly in the Agent Portal, such as Repayment Term Extensions. This includes both applying a new Repayment Term Extension as well as editing an existing one. The length of the extension can also be viewed in the Agent Portal.

Processors can add and/or update customer applications in the Application Status tab in the Account Activity card of the Agent Portal.

Customers can view the status of any applications Nelnet has received when they log into the customer portal. This includes, but is not limited to, the status of any deferment, forbearance, loan modification, or fraud applications. These statuses also display whether the borrower has an application pending for (or is repaying under) an alternative repayment plan, listing the plan chosen; and whether the borrower has an application pending for any loan forgiveness benefit. Applications for items such as Death Request, Fraud/ID Theft Request, and Qualified Requests will not display to the customer.

## Business logic

The goal of a loan modification is to provide the borrower with more favorable terms that better align with their current financial situation, making it easier for them to repay the loan.

## Workflow

Velocity completes the following steps based on the loan modification settings when adding a loan modification.

1. Functions performed to the loan when the corresponding options are configured for a Loan Modification setting:
2. Mark the loan modification status as Processing.
3. Process interest rate reduction if required, using either a flat rate or percentage reduction:
    * Flat rate - specifies the exact interest rate
    * Percentage - specifies the percentage reduction (for example, .025 percent reduction)
4. Payment amount reduction if required, using one of the options listed:
    * Dollar - a specific dollar amount reduction (for example, reduce the payment by $10)
    * Percentage - a specific percentage reduction (for example, reduce the payment by 10%)
    * Fixed payment - sets payments to a specific dollar amount (for example, the payment will be $100)
5. Bring the loan current
6. Snapshot
7. Replay - if effectiveDate was in the past
8. Capitalize interest.
9. Reamortize the loan.
10. If applicable to the loan mod: 
    * An activity note is created
        * Type - Event
        * Activity - Loan Term Modified (example)
        * Details (example)
            * Extend: Term modification applied. Maturity date updated from ${beforeMaturityDate} to ${afterMaturityDate}. Term extended by ${count}. Remaining Term updated from ${beforeRemainingTerm} to ${afterRemainingTerm}. for all 3 scenarios: Add, Edit, and Remove.
            * Reduce: Term modification applied. Maturity date updated from ${beforeMaturityDate} to ${afterMaturityDate}. Term reduced by ${count}. Remaining Term updated from ${beforeRemainingTerm} to ${afterRemainingTerm}. for all 3 scenarios: Add, Edit, and Remove.
    * Created By - User token
11. Mark steps as Completed.
12. Mark loan mod status as Active.

## Examples

**Interest Rate Reduction**: The lender may agree to lower the interest rate on the loan, which can help reduce the borrower's monthly payments and overall interest costs.


**Loan Term Extension**: The lender may extend the repayment term of the loan, spreading out the remaining balance over a longer period. This can lower the monthly payments but may result in paying more interest over the life of the loan.


**Principal Forbearance**: In certain cases, the lender may agree to temporarily reduce or suspend a portion of the principal balance owed. This provides immediate relief to the borrower by reducing the monthly payment amount, but the deferred amount will typically need to be repaid later.


**Payment Deferral**: The lender may allow the borrower to skip a certain number of monthly payments and add them to the end of the loan term, effectively extending the repayment period without incurring penalties.

## Processing

See Workflow.

## Lender configuration

Lenders determine which loan modifications to offer in their loan programs. Loan modifications are configured on the System Configuration Portal.

Current options include:

* interest rate reduction
* payment amount reduction
* term extension

These can be permanent or temporary. The lender can also choose to bring the loan current or backdate the changes when adding the loan modification and to capitalize interest or re-amortize at the end of the loan modification.

Examples include:

* Loan payment may change by a certain amount
* Customer’s past due status
* Customer’s on-time payment record
* Customer having a set payment amount or flexible payment by loan

In the System Configuration Portal, the Lender defines the settings for each of the Loan Modifications.