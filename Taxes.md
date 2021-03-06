# Base System Support for Taxes

If your tax requirements are simple then the base system tax is the easiest approach for you.

The base system of OSPOS includes support for a maximum of two tax rates for each item.  Taxes are treated as a sales tax or it can be treated as a value added tax (tax included) - it cannot be mixed.  Whether or not it is to be treated as a sales tax or a VAT tax is established up front.  After sales are made any attempt to switch between the two will result in incorrect numbers in your reports.


# Destination Based Tax

In the United States the sales tax to be collected can be based on the origin address, ship to address, or bill to address (if the product is being shipped).   The rules for collecting taxes are governed by the taxing jurisdiction.

If you need to collect and report taxes by multiple tax jurisdictions then the Destination Based Tax feature is a good fit for you. 


# India Goods and Services Tax

In 2017 India introduced new tax reporting laws that have similar requirements to the US Destination Based Sales Tax system.

More information about configuring the Destination Based Tax feature specifically to support India GST can be found at [More about India GST](India-GST).


# Definitions

**Default Tax Code** The default tax code represents the group of tax jurisdictions where the store is located.  There can only be one default tax code for each company.  Currently OSPOS only allows for a single company (although there are plans to make it multi-company).  The default tax code is a configured option. If and when multi-company is supported the default tax code will need to be configured at the store level. This is also known as the Origin Tax Code.

**HSN Code** HSN code or Harmonized System Nomenclature code number is an internationally adopted commodity description and coding system developed by the World Customs Organization (WCO).

**Tax Code** A code assigned to a customer that identifies the group of taxing jurisdictions which should be applied to the sale.  

**Tax Rate** The tax rate is a percent value supporting up to 4 decimal places.

**Item Tax Category** A given tax jurisdiction has a standard tax, but some products might require a different tax rate (for example alcohol products might have a higher sales tax rate).  To accomplish that, if a taxing jurisdiction requires a different tax rate for a particular category of items then those items must be associated with that category. For India GST the tax category centers around the Harmonized Tariff Schedule (HTS) product categories.

**VAT Tax**  The taxes are tracked not just for sales but also as part of for receiving.

**Tax Included** The tax is included in the sales price.

**Tax Excluded** The tax is NOT included in the sales price and is

**Taxing Decimals** The tax amount is computed for each tax group for each item on the invoice.  The taxing decimals indicates how many decimals the tax amount will be stored as.  The tax amount at this level will be rounded according to the rounding code.  Then when the sale is "complete" the tax amount of each item in the same tax group is accumulated and that total is rounded to the number of decimals specified by the currency decimals configuration value using the specified rounding rule (as determined by the primary taxing authority).

**Cascaded Tax** Some VAT tax locations require that taxes be "cascaded".  This means that the 2nd tax amount is computed using the total of the invoice and the tax amount computed using the 1st tax.  Cascaded sales tax is not currently supported.  However, database changes have already been made to support it, so if anyone wishes to work with me to test and use this feature then it shouldn't be too much of an effort to add it.

**Tax Group** A tax group represents the summary of taxes to be collected for a particular sale, for one or more tax authorities that have agreed to be collected at the same time as a group (even though for purpose of tax reporting they might be reported independently).  (i.e. state, county, city, etc).  At this point in time all U.S. tax laws that I know about allow the individual tax jurisdiction tax rates to be added and collected as a single tax rate.  If this is to be the case then flag the tax code for single rate taxing or simply define a single jurisdiction that represents the combined jurisdictions.  India needs to report taxes collected by jurisdiction. 


# Rules and Constraints

**Once the Destination Tax feature is enabled, the current default tax rate fields will not be used for the purpose of calculating taxes.** OSPOS currently has two default tax percent fields.  When this module is enabled these will not be used.

**Use origin tax code if there isn't a tax code assigned to the customer.** If there isn't a tax code for the customer then the Origin Tax Code will be used to calculate the tax for the order.  It will be retrieved using the tax code configured as the default. 

**The customer tax origin basis depends on the register mode.** If the register mode is "Sales by Receipt" then tax will be computed based on the default tax code. If the sale is "Sales by Invoice" then tax will be computed based on the city and state of the customer address.

**Tax rates should be locked in when sale is completed.** When an invoice is reprinted it needs to be able to calculate tax based on the tax rates that were in place when the invoice was originally printed.


# Rules of Operation

## Configuring for Destination Based Taxing

You are not required to immediately start using the destination based tax module.  Your current tax setup should continue to work.  If you use "tax included" pricing it should also continue to operate without any intrusive changes.  If either of those statements are false then please report the bug.

Under the General Configuration tab the "Tax Included" option has a lot of power.  If selected then all reports assume that taxes are calculated assuming that the taxes are VAT taxes.  Deselecting "Tax Included" changes all reports to assume that all taxes are sales taxes.  To use customer sales tax be sure that this option is deselected.

Under the General Configuration tab the "Destination Based Tax Support" will need to be selected in order to use the new Tax module to compute taxes.  If it's not selected then the system will continue to use the tax percents added to the item table.

To be able to add a destination based tax you will need to authorize the employee to the Taxes module.  Go to the employee permissions page and select the "Taxes" module. There are two check boxes labeled Taxes.  Be sure to select the Tax module and not the Tax reporting option.

## Adding a New Sales Tax

An employee must be authorized to the tax module to be able to set up tax rates.

The following information is provided for each tax.  You should always set up the tax code definition for the store location (a.k.a. Origin Tax).  You'll then enter this tax code on the general configuration page (Default Origin Tax Code) 

**Tax Code** A code is assigned to each tax jurisdiction that you want to collect and report taxes on.  The code will generally indicate the geographical location that tax applies to and is assigned by the user.   Make a note of the tax code to be used for store sales because that is referred to as the Origin tax code and should be added to the General Configuration tab for Default Origin Tax Code.

**Tax Code Name** This is just an additional description used to elaborate on the code if you are using abbreviations for your Tax Code.

**Tax Code Type** This establishes how the tax is calculated.  The options are "Sales Tax" and "Sales Tax by Invoice".  "Sales Tax" is used to indicate that the sales tax is calculated at a item level and that calculated amount is totaled and rounded to determine the amount collected.  "Sales Tax by Invoice" indicates that the extended amount for each item sold is accumulated for a tax category and then the tax rate is applied and the rounded amount becomes the total amount calculated.  Which approach is selected is usually determined by the tax regulations of the taxing authority.

**City** and **State** The city and state can be used to identify the applicable tax code.  If the customer information includes a specific tax code then the tax for that code will be used. Otherwise, if the customer information includes the city and state then the city and state will be used to find the tax code.  If there isn't a tax code for the combination of city and state, then the tax code for the state will be used.  If there isn't one for the state then the default origin tax code will be used.

**Tax Rate** This is the sales tax rate that will be used to compute taxes for the given tax code.  If there are multiple tax jurisdictions the tax rates can be added together for the purpose of compute tax rates.  They would need to be split out later for the purpose of reporting taxes.

**Rounding Code** This will establish how fractional tax amounts should be rounded.

**Category Exceptions**  The standard sales tax can be overridden for a particular tax category of items.  For example spirits, liquor and beer often have a higher tax rate.  Service items are often non-taxable.  This is implemented by assigning the tax category to the item and then adding the tax category exception to the tax rate definition.


# Comments


# Change History
* 6/13/2018 - Started adding documentation for India's Goods and Services Tax 
* 4/15/2020 - Made a few corrections to the page.