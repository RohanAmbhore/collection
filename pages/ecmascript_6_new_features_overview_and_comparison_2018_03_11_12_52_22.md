<a href="http://es6-features.org/#CurrencyFormatting">http://es6-features.org/#CurrencyFormatting</a><div id="articleHeader"><h1>Overview and Comparison</h1></div>    <div>Internationalization & Localization</div>
    <div>Currency Formatting</div>
    <div>Format numbers with digit grouping, localized separators and attached currency symbol.</div>
<div>
    <div><b>ECMAScript 6</b> — syntactic sugar: reduced | traditional</div>
    <div>var l10nUSD = new Intl.NumberFormat("en-US", { style: "currency", currency: "USD" })
var l10nGBP = new Intl.NumberFormat("en-GB", { style: "currency", currency: "GBP" })
var l10nEUR = new Intl.NumberFormat("de-DE", { style: "currency", currency: "EUR" })
l10nUSD.format(100200300.40) === "$100,200,300.40"
l10nGBP.format(100200300.40) === "£100,200,300.40"
l10nEUR.format(100200300.40) === "100.200.300,40 €"
</div>
    
    
</div>
    <div>
    <div><b>ECMAScript 5</b> — syntactic sugar: reduced | traditional</div>
    <div>// no equivalent in ES5</div>
    
    
</div>
