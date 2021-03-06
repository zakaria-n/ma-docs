.. include:: ../../toc_default.txt


Order Delivery
###############

Order delivery is supposed to be called when the order or specific item has been sent to the customer. Hence this call marks specified orderrows as delivered. When all orderrows have been delivered an invoice is automatically created. Keep in mind that if there is a delivery fee associated with the order this will show up as a separate orderrow with the productid 'Postage'. This must also be set as delivered for the order to be considered fully delivered.


Request Example - JSON
======================

.. code-block:: json

	{
	  "OrderId": 1,
	  "Products": [
		{
		  "OrderRowId": 1,
		  "QuantityToDeliver": 2,
		  "PackageId": "sample string 3",
		  "PackageCarrierId": 1
		},
		{
		  "OrderRowId": 1,
		  "QuantityToDeliver": 2,
		  "PackageId": "sample string 3",
		  "PackageCarrierId": 1
		}
	  ]
	}



Request Attributes
==================

.. _table-order-request-attributes:

+-----------------------+-------------+----------------------------------------------------------------------------------------------------+------------+
| Variable              | Type        | Description                                                                                        | Required   |
+=======================+=============+====================================================================================================+============+
| OrderId               | integer     | An id which refers to your order and store in the Marketplace.                                     | Yes        |
+-----------------------+-------------+----------------------------------------------------------------------------------------------------+------------+
| OrderRowId            | integer     | Refers to the order row associated to a specific order.                                            | Yes        |
+-----------------------+-------------+----------------------------------------------------------------------------------------------------+------------+
| QuantityToDeliver     | integer     | Indicates how many products you intend to set as delivered for the specific order row.             | Yes        |
+-----------------------+-------------+----------------------------------------------------------------------------------------------------+------------+
| PackageId             | string      | Allows the customer to track the deliver. Also included in the delivery mail sent to the customer. | No         |
+-----------------------+-------------+----------------------------------------------------------------------------------------------------+------------+
| PackageCarrierId      | integer     | The id of the carrier used to ship the package (e.g. Posten, DHL).                                 | No         |
+-----------------------+-------------+----------------------------------------------------------------------------------------------------+------------+

.. ATTENTION::
	An updated list of available packagecarriers and their id can be retrieved by performing a GET request to api/packagecarrier.


Response Example - json:
========================
This request returns an http status code, indicating how the call went, where the desired result is OK (200), including a comprehensive list of order details and invoice information.

.. code-block:: json

	{
	  "OrderDetails": {
		 "OrderKey": "c6840daf-6163-45ef-adce-7f5e8d8f2afe-42277358",
		 "OrderId": 42277358,
		 "State": "Invoiced",
		 "PaymentStatus": "AwaitingPayment",
		 "CreatedDateUtc": "2014-02-07T19:22:48.5942457",
		 "LastModifiedDateUtc": "2014-02-07T19:22:48.5942457",
		 "MerchantId": "3b1addb2-2b6f-49bc-a185-2b5cfb445d66",
		 "CountryCode": "Sweden",
		 "CurrencyCode": "SEK",
		 "TotalAmount": 1495.0,
		 "TotalAmountExcludingVat": 1196.0,
		 "TotalSalesAmount": 1495.0,
		 "CustomerInfo": {
		   "CustomerId": 62880501,
		   "EmailAddress": "",
		   "ShippingAddress": {
		     "Name": "Testperson",
		     "StreetAddress": "Stårgatan 1xa",
		     "CoAddress": "",
		     "ZipCode": "12345",
		     "City": "Ankeborg",
		     "Country": "SE"
		   },
		   "BillingAddress": {
		     "Name": "Testperson",
		     "StreetAddress": "Stårgatan 1xa",
		     "CoAddress": "",
		     "ZipCode": "12345",
		     "City": "Ankeborg",
		     "Country": "SE"
		   },
		   "Phones": {
		     "PhoneMobile": "0703013319",
		     "PhoneWork": null,
		     "PhoneHome": null
		   }
		 },
		 "OrderRows": [
		 {
		   "OrderRowId": 1,
		   "FulfillmentStatus": "Invoiced",
		   "PaymentStatus": "AwaitingPayment",
		   "ProductId": "ART000494",
		   "ProductName": "Star wars",
		   "ProductType": "Article",
		   "Quantity": 1,
		   "DeliveredQuantity": 1,
		   "InvoicedQuantity": 1,
		   "CancelledQuantity": 0,
		   "ReturnedQuantity": 0,
		   "PickedQuantity": null,
		   "PricePerUnit": 1495.0,
		   "OrdinaryPricePerUnit": 1495.0,
		   "VatPerUnit": 299.0,
		   "VatPercentage": 25.0000,
		   "PackageId": "test",
		   "DebitedAmount": 1495.0,
		   "CreditedAmount": 0.0,
		   "PaidAmount": 0.0,
		   "RefundedAmount": 0.0,
		   "AddonToProductId": null
		 }
	],
		 "InvoiceNumbers": [
		   "1000052"
		 ],
		   "TotalVat": 299.0
		 },
		 "invoices": [
		 {
		   "Rows": [
		 {
		   "TotalPaymentAmount": 0.0,
		   "TotalCreditNoteAmount": 0.0,
		   "Status": "AwaitingPayment",
		   "InvoiceRowNumber": 1,
		   "OrderRowId": 1,
		   "ProductId": "ART000494",
		   "ProductName": "Star wars",
		   "ProductType": "Article",
		   "Quantity": 1,
		   "PricePerUnit": 1495.0,
		   "VatPerUnit": 299.0,
		   "VatPercentage": 25.0000,
		   "TotalAmount": 1495.0,
		   "TotalVat": 299.0
		 }
		 ],
		 "Status": "AwaitingPayment",
		 "Payments": null,
		 "InvoiceNumber": "1000052",
		 "MerchantId": "3b1addb2-2b6f-49bc-a185-2b5cfb445d66",
		 "OrderId": 42277358,
		 "CustomerId": 62880501,
		 "CreatedDateUtc": "2014-02-07T12:29:12.8663761Z",
		 "BookingDateUtc": "2014-02-07T12:29:12.8663761Z",
		 "TotalAmount": 1495.0,
		 "TotalVat": 299.0,
		 "CurrencyCode": "SEK"
		 }
	  ]
	}



Response Attributes
===================

.. _table-order-response-attributes:

+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| Variable                     | Type        | Description                                                                                         |
+==============================+=============+=====================================================================================================+
| OrderKey                     | string      | Your unique order identifier. Composition of merchant id and order id.                              |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| OrderId                      | integer     | An id which refers to your order and store in the Marketplace.                                      |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| FulfillmentStatus/State      | enum        | Indicates the state of the order or order row. Available states are:                                |
|                              |             |    Pending = 0                                                                                      |
|                              |             |    Delivered = 1                                                                                    |
|                              |             |    Cancelled = 2                                                                                    |
|                              |             |    Returned = 3                                                                                     |
|                              |             |    Invoiced = 4                                                                                     |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| PaymentStatus                | enum        | Indicates the state of the payment. Available states are:                                           |
|                              |             |    NotApplicable = 0                                                                                |
|                              |             |    AwaitingPayment = 1                                                                              |
|                              |             |    Paid = 2                                                                                         |
|                              |             |    AwaitingRefund = 3                                                                               |
|                              |             |    Refunded = 4                                                                                     |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| CreatedDateUtc               | datetime    | The date and time the order was placed on CDON.                                                     |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| MerchantId                   | string      | Your unique merchant identifier.                                                                    |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| CountryCode                  | string      | Country of the order, indicating in what channel the order was placed.                              |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| CurrencyCode                 | string      | Currency code for the order.                                                                        |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| TotalAmount                  | decimal     | The total amount of the order. Including VAT.                                                       |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| TotalAmountExcludingVat      | decimal     | The total amount excluding VAT.                                                                     |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| TotalSalesAmount             | decimal     | The total amout of the order including VAT and other fees.                                          |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| CustomerId                   | integer     | A customer’s unique identifier                                                                      |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| EmailAddress                 | string      | Hidden field.                                                                                       |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| Name                         | string      | Customers name. May include surname.                                                                |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| StreetAddress                | string      | Customer’s street address. Applies to Shipping- and Billing address.                                |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| CoAddress                    | string      | Customer’s in care of address. Applies to Shipping- and Billing address.                            |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| ZipCode                      | string      | Customer´s zip code.                                                                                |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| City                         | string      | Customer´s city.                                                                                    |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| Country                      | string      | Customer´s country.                                                                                 |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| PhoneMobile                  | string      | Customer’s mobile phone number.                                                                     |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| PhoneWork                    | string      | Customer’s work phone number.                                                                       |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| PhoneHome                    | string      | Customer’s home phone number.                                                                       |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| OrderRowId                   | integer     | Refers to the order row associated to a specific order.                                             |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| ProductId                    | string      | Merchants own unique product identifier.                                                            |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| AddonToProductId             | string      | Indicates that this product is an add-on to different product in the order.                         |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| ProductName                  | string      | Merchants product title.                                                                            |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| ProductType                  | enum        | Indicated the type of the product. Available types are:                                             |
|                              |             |    Article = 0                                                                                      |
|                              |             |    Service = 1                                                                                      |
|                              |             |    Postage = 2                                                                                      |
|                              |             |    Fee = 3                                                                                          |
|                              |             |    Compensation = 4                                                                                 |
+------------------------------+-------------+-----------------------------------------------------------------------------------------------------+
| Quantity                     | integer      | Indicates the total quantity ordered for a specific product.                                       |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| DeliveredQuantity            | integer      | Indicates the delivered quantity. May not exceed quantity.                                         |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| InvoicedQuantity             | integer      | Indicates the invoiced quantity. May not exceed quantity.                                          |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| CancelledQuantity            | integer      | Indicates the cancelled quantity. May not exceed quantity                                          |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| ReturnedQuantity             | integer      | Indicates the returned quantity. May not exceed quantity.                                          |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| PickedQuantity               | integer(null)| Indicates the picked quantity. May not exceed quantity. Can be null.                               |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| PricePerUnit                 | decimal      | Sales price for the product.                                                                       |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| OrdinaryPricePerUnit         | decimal      | Ordinary price for the product. If the sales price is lower this will be seen as a discount and    |
|                              |              | will be displayed as such on CDON.                                                                 |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| VatPerUnit                   | decimal      | VAT for the product.                                                                               |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| VatPercentage                | string       | VAT as percentage for the product.                                                                 |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| PackageId                    | string       | Allows the customer to track the deliver. Also included in the delivery mail sent to the customer. |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| DebitedAmount                | decimal      | The amount the customer needs to pay associated to an invoice.                                     |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| CreditedAmount               | decimal      | The amount that gets refunded to the customer associated to an invoice.                            |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| PaidAmount                   | decimal      | The amount that has already been paid.                                                             |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| RefundedAmount               | decimal      | The refunded amount in case of return.                                                             |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| InvoiceNumber                | string       | The invoice number associated with the order and delivery.                                         |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| TotalVat                     | decimal      | The total order VAT.                                                                               |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| TotalPaymentAmount           | decimal      | The total amount the customer needs to pay.                                                        |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| TotalCreditNoteAmount        | decimal      | The total amount that needs to be refunded to the customer.                                        |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| InvoiceRowNumber             | string       | Refers to the invoice number associated to a specific order.                                       |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
| BookingDateUtc               | datetime     | Invoice booking date. The date the debt is booked.                                                 |
+------------------------------+--------------+----------------------------------------------------------------------------------------------------+
