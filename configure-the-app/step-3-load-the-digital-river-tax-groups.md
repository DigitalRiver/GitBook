---
description: Learn how to load the Digital River tax groups.
---

# Step 3: Load the Digital River tax groups

Load the Digital River-supported tax groups in the merchant system for determining the tax code for SKU creation. See [setting-the-tax-code](https://docs.digitalriver.com/digital-river-api/product-management/creating-and-updating-skus#tax-code) for more details related to tax groups and types.&#x20;

To load and execute the existing tax groups from Digital River, use the `ImpEx` script below.

```
INSERT_UPDATE DRTaxGroup;taxGroup[unique=true]

;Downloadable Goods (Non-Software)

";Food, Beverage & Household"

;Physical Goods

;Services & Miscellaneous

;Software (Downloadable & Physical)

;Warranties


INSERT_UPDATE DRTax;drCode[unique=true];drTaxType;taxGroup(taxGroup)

;4512.100;Digital Image;Downloadable Goods (Non-Software)

;55111509.12;Virtual Goods;Downloadable Goods (Non-Software)

;55111512.100;Music;Downloadable Goods (Non-Software)

;55111507.120;Electronic Newspapers (Includes Subscriptions);
Downloadable Goods (Non-Software)

;55111506.120;Electronic Magazines (Includes Subscriptions);
Downloadable Goods (Non-Software)

;55111513.120;Educational / Vocational Texts;Downloadable Goods (Non-Software)

;55111502.120;eBooks;Downloadable Goods (Non-Software)

";51191905;Non-Prescription Vitamins;Food, Beverage & Household"

";5124;Non-Prescription Drugs;Food, Beverage & Household"

";47;Miscellaneous Supplies;Food, Beverage & Household"

";50;Food - General;Food, Beverage & Household"

;531316.150;Automatic Blood Pressure Monitors;Physical Goods

;52141545.100;Energy Star - Stove;Physical Goods

;4010.200;Energy Star - Dehumidifier;Physical Goods

;4010.100;Energy Star - Air Conditioner;Physical Goods

;40101609.100;Energy Star - Ceiling Fan;Physical Goods

;39101629.100;Energy Star - Light Bulbs;Physical Goods

;52141506.100;Energy Star - Freezer;Physical Goods

;52141501.100;Energy Star - Refrigerator;Physical Goods

;52141601.100;Energy Star - Washer;Physical Goods

;52141602.100;Energy Star - Dryer;Physical Goods

;52141505.100;Energy Star - Dishwasher;Physical Goods

;4321_S;Computer Supplies - Subscription;Physical Goods

;43211509;Mobile Devices;Physical Goods

;42;Medical Equipment;Physical Goods

";4512;Consumer Electronics (Photographic, Filming, or Video Equipment);
Physical Goods"

";52161500_C;Consumer Electronics (T.V., Monitor, Display) - 
Size (>4""<15"");Physical Goods"

";52161500_B;Consumer Electronics (T.V., Monitor, Display) - 
Size (= or >35"");Physical Goods"

";52161500_A;Consumer Electronics (T.V., Monitor, Display) - 
Size (= or >15""<35"");Physical Goods"

;601410;Video Game Consoles and Accessories;Physical Goods

;531027;Uniforms;Physical Goods

;49;Sports and Recreation Equipment;Physical Goods

;441216;School Supplies;Physical Goods

;6010;School Instructional Materials;Physical Goods

;461815.100;Safety Clothing (Not Suitable for Everyday Use);Physical Goods

;5510;Printed Media (Non-Subscription);Physical Goods

;55101504.100;Newspapers (Includes Subscription);Physical Goods

;55101506.100;Magazines (Includes Subscriptions);Physical Goods

;601410;General Merchandise;Physical Goods

;5216;Consumer Electronics (Non-Computer);Physical Goods

;4321_A;Computers;Physical Goods

;4321_C;Computer Supplies;Physical Goods

;4321_B;Computer Peripheral Devices;Physical Goods

;55101510;Books - General Purpose;Physical Goods

;55101509;Books - Educational and Vocational Texts;Physical Goods

;53121603;Backpacks;Physical Goods

;531029.100;Apparel & Footwear (Everyday Use);Physical Goods

;531029.200;Apparel & Footwear (Athletic Use);Physical Goods

;70.360;Installation Service Charges Provided by the Seller of TPP;
Services & Miscellaneous

";81112201.121;Mandatory Maintenance Agreements - Services and Upgrades, 
Only for Downloadable;Services & Miscellaneous"

;8111;Computer Services;Services & Miscellaneous

;70.60;Consulting Services;Services & Miscellaneous

;70.100;General Services;Services & Miscellaneous

;70.120;Gift Cards;Services & Miscellaneous

";81112201.120;Mandatory Maintenance Agreements - Services and Upgrades, 
for Downloadable and Physical Products;Services & Miscellaneous"

;70.150;Non-warranty Repairs;Services & Miscellaneous

;811121;Online Data Storage;Services & Miscellaneous

";81112201.420;Optional Maintenance Agreements - Services and Upgrades, 
for Downloadable Products;Services & Miscellaneous"

";81112201.410;Optional Maintenance Agreements - Services and Upgrades, 
for Physical Products;Services & Miscellaneous"

";81112201.200;Optional Maintenance Agreements - Services Only, 
for Downloadable and Physical Products;Services & Miscellaneous"

;70.300;Seminar Classes;Services & Miscellaneous

;70.280;Software Training;Services & Miscellaneous

;811118.100;Technical Support;Services & Miscellaneous

;70.120_A;Virtual Currency;Services & Miscellaneous

;70.220;Membership Dues - General;Services & Miscellaneous

;70.222;Membership Dues & Professional Organization;Services & Miscellaneous

;81112105;Web Hosting;Services & Miscellaneous

;4323.310_B;Backup Media (CD/DVD) - One Disc per Order;Software 
(Downloadable & Physical)

;81112106;Software as a Service;Software (Downloadable & Physical)

;4323.310_E;Physical Software (Gaming Only);Software (Downloadable & Physical)

;4323.310_A;Physical Software (Non-Gaming);Software (Downloadable & Physical)

;4323.310_D;Physical Media Kits;Software (Downloadable & Physical)

;4323.310_C;Backup Media (CD/DVD) - One Disc per Product;Software 
(Downloadable & Physical)

;4323.320_C;Downloadable Media Kits;Software (Downloadable & Physical)

;4323.320_D;Downloadable Software (Gaming Only);Software (Downloadable & Physical)

";4323.320_A;Downloadable Software (Non-Gaming, Includes Software Subscriptions);
Software (Downloadable & Physical)"

;4323.320_B;Extended Download Service;Software (Downloadable & Physical)

";95.210;Optional Warranties - Purchased at Time of Sale of for Consumer Goods, 
Labor Only;Warranties"

";95.222;Optional Warranties - NOT Purchased at Time of Sale of for Consumer Goods,
Parts & Labor;Warranties"

";95.220;Optional Warranties - NOT Purchased at Time of Sale of for Consumer Goods,
Labor Only;Warranties"

;95.100;Mandatory Warranties;Warranties

";95.212;Optional Warranties - Purchased at Time of Sale of for Consumer Goods,
Parts & Labor;Warranties"

```

