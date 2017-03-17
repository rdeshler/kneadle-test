# kneadle-test
Test for docs generator

## Test
* TEST 1
* TEST 2
* TEST 3
* TEST 4
<pre><code>&lt;blockquote&gt;
    &lt;p&gt;For example.&lt;/p&gt;
&lt;/blockquote&gt;
</code></pre>

<p>Test</p>
<p>The <em>Transaction Management Service (TMS)</em> provides read-only access to merchant transaction data stored in the Commerce Web Services (CWS) transaction database. TMS eliminates the need for the merchant application to store transaction data locally by providing access to merchant transaction data for transaction reporting purposes, as well as for processing subsequent transactions, such as incremental authorizations, voids, returns, and batch settlement processing.</p>
<p>Transaction management functionality is supported by the Transaction Management Service (TMS) and corresponding <em>Transaction Management API</em>. The TMS API makes use of both Service Keys and sign-on authentication credentials to ensure safe, secure access to CWS transaction data.</p>
<p>The integration of the TMS API provides the following benefits:</p>
<ul>
<li><strong>Access to all Bankcard transaction data</strong> – All Bankcard transaction classes and types are accessible.</li>
<li><strong>Two levels of transaction detail</strong> – On a per query basis, you can specify whether summary or detailed transaction information should be retrieved.</li>
<li><strong>Variety of search/filter criteria</strong> – Enables greater precision and faster response times by limiting the data returned to only that which is required.</li>
<li><strong>Identification of transaction families</strong> – Authorizations or returns followed by subsequent transactions are linked using a parent ID. This allows all related transaction data to be returned in the context of the entire transaction family.</li>
</ul>
<p class="note"><strong>Note:</strong> The integration of the Transaction Management Service (TMS) API is optional.</p>
<p> </p>
<hr>
<p> </p>
<p>The Transaction Management API provides a simple set of operations that allow you to retrieve two levels of transaction data-<em>summary</em> and <em>detail</em>.</p>
<ul>
<li><strong>Summary</strong> – Sufficient to perform subsequent transaction processing (<span class="codeInline">Adjust</span>, <span class="codeInline">Undo</span>, <span class="codeInline">ReturnById</span>, etc.). Summary data is returned in the context of the transaction family.</li>
<li><strong>Detail</strong> – Summary data in addition to all data collected and stored about the transaction. Detail data is a complete set of CWS Bankcard transaction request, response, merchant and application data, and additional metadata. This data can be formatted as either a serialized string or as a data record.</li>
</ul>
<p> </p>
<hr>
<p> </p>
<h3 id="QueryBatch">QueryBatch</h3>
<p>The <span class="codeInline">QueryBatch</span> operation queries the batch summary and returns Batch Status, DateTime, and a list of <span class="codeInline">transactionId</span>s in the batch.</p>
<p class="note"><strong>Note:</strong> The <span class="codeInline">QueryBatch</span> operation is only supported in Terminal Capture environments.</p>
<h2>SOAP</h2>
<h4>Operation</h4>
<p class="codeBox">List&lt;BatchDetailData&gt; QueryBatch(string sessionToken, QueryBatchParameters queryBatchParameters, PagingParameters pagingParameters);</p>
<h4>Parameters</h4>
<table class="table">
<tbody>
<tr>
<td class="tableHead">Parameter</td>
<td class="tableHead">Data Type</td>
<td class="tableHead">Description</td>
</tr>
<tr>
<td><span class="codeInline">sessionToken</span></td>
<td>String</td>
<td>The short-lived token used to authenticate to CWS.</td>
</tr>
<tr>
<td><span class="codeInline">queryBatchParameters</span></td>
<td><a class="codeInline" href="/hc/en-us/articles/203020418"> QueryBatchParameters</a></td>
<td>The batch query details.</td>
</tr>
<tr>
<td><span class="codeInline">pagingParameters</span></td>
<td><a class="codeInline" href="/hc/en-us/articles/202567933-Data-Services-Data-Elements" target="_blank">PagingParameters</a></td>
<td>Defines the parameters for the service to use for paging large datasets.</td>
</tr>
</tbody>
</table>
<p class="note"><strong>Note:</strong> When specifying <span class="codeInline">DateRange</span> in <span class="codeInline">QueryBatchParameters</span>, the range must be within the last 90 days or a fault is thrown. Regardless of how <span class="codeInline">DateRange</span> is specified, only the matching <span class="codeInline">transactionId</span>s within the last 90 days are returned.</p>
<h4>Return Type</h4>
<table class="table">
<tbody>
<tr>
<td class="tableHead">Data Type</td>
<td class="tableHead">Description</td>
</tr>
<tr>
<td>List&lt;<a class="codeInline" href="/hc/en-us/articles/203020418">BatchDetailData</a>&gt;</td>
<td>Collection of batch details.</td>
</tr>
</tbody>
</table>
<h4>Exceptions</h4>
<table class="table">
<tbody>
<tr>
<td><span class="codeInline">AuthenticationFault</span></td>
<td><span class="codeInline">TMSTransactionFailedFault</span></td>
</tr>
<tr>
<td><span class="codeInline">ExpiredTokenFault</span></td>
<td><span class="codeInline">TMSUnavailableFault</span></td>
</tr>
<tr>
<td><span class="codeInline">InvalidTokenFault</span></td>
<td><span class="codeInline">TMSUnknownServiceKeyFault</span></td>
</tr>
<tr>
<td><span class="codeInline">TMSOperationNotSupportedFault</span></td>
<td><span class="codeInline">TMSValidationResultFault</span></td>
</tr>
</tbody>
</table>
<p class="imageFigureText">For additional details about the Transaction Management faults listed above, refer to the <a href="/hc/en-us/articles/202484146--Transaction-Management-Fault-Reference">Transaction Management Fault Reference</a>.</p>
<h2>REST</h2>
<p class="note"><strong>Note:</strong> The <a href="/hc/en-us/articles/203497757-REST-Information">HTTP Authorization Header</a> must contain the required <span class="codeInline">sessionToken</span> value.</p>
<h4>Operation</h4>
<table class="table">
<tbody>
<tr>
<td><strong>URL</strong></td>
<td>https://api.cert.nabcommerce.com/REST/2.0.18/DataServices/TMS/batch</td>
</tr>
<tr>
<td><strong>Action</strong></td>
<td>POST</td>
</tr>
</tbody>
</table>
<h4>Parameters</h4>
<p>None.</p>
<h4>Message Body Type</h4>
<table class="table">
<tbody>
<tr>
<td class="tableHead">Data Type</td>
<td class="tableHead">Description</td>
</tr>
<tr>
<td><a class="codeInline" href="/hc/en-us/articles/203020438-Transaction-Management-REST-Data-Elements">QueryBatch</a></td>
<td>Body type for REST Query Batch operation.</td>
</tr>
</tbody>
</table>
<h4>Return Type</h4>
<table class="table">
<tbody>
<tr>
<td class="tableHead">Data Type</td>
<td class="tableHead">Description</td>
</tr>
<tr>
<td>List&lt;<a class="codeInline" href="/hc/en-us/articles/203020418">BatchDetailData</a>&gt;</td>
<td>Collection of batch details.</td>
</tr>
</tbody>
</table>
<h4>Exceptions</h4>
<table class="table">
<tbody>
<tr>
<td><span class="codeInline">AuthenticationFault</span></td>
<td><span class="codeInline">TMSTransactionFailedFault</span></td>
</tr>
<tr>
<td><span class="codeInline">ExpiredTokenFault</span></td>
<td><span class="codeInline">TMSUnavailableFault</span></td>
</tr>
<tr>
<td><span class="codeInline">InvalidTokenFault</span></td>
<td><span class="codeInline">TMSUnknownServiceKeyFault</span></td>
</tr>
<tr>
<td><span class="codeInline">TMSOperationNotSupportedFault</span></td>
<td><span class="codeInline">TMSValidationResultFault</span></td>
</tr>
</tbody>
</table>
