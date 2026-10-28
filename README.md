
=LET(
id,$D2,
ro,$A2,
cf,$B2,
persona,$C2,
src,SWITCH(TRUE,
ISNUMBER(SEARCH("POs & PO Conversion",id)),'POs & PO Conversion'!$A$1:$AZ$1000,
ISNUMBER(SEARCH("Payables & Invoicing",id)),'Payables & Invoicing'!$A$1:$AZ$1000,
ISNUMBER(SEARCH("Fieldglass Services SES",id)),'Fieldglass Services SES'!$A$1:$AZ$1000),
sessionCol,XMATCH(id,TAKE(src,1),0),
data,DROP(src,2),
matchRow,XMATCH(1,(CHOOSECOLS(data,1)=ro)*(CHOOSECOLS(data,2)=cf)*(CHOOSECOLS(data,3)=persona),0),
IFERROR(INDEX(data,matchRow,sessionCol),"")
)




=LET(
id,$D2,
ro,$A2,
cf,$B2,
persona,$C2,
src,SWITCH(TRUE,
ISNUMBER(SEARCH("POs & PO Conversion",id)),'POs & PO Conversion'!$A$1:$AZ$1000,
ISNUMBER(SEARCH("Payables & Invoicing",id)),'Payables & Invoicing'!$A$1:$AZ$1000,
ISNUMBER(SEARCH("Fieldglass Services SES",id)),'Fieldglass Services SES'!$A$1:$AZ$1000),
sessionCol,XMATCH(id,TAKE(src,1),0),
data,DROP(src,2),
matchRow,XMATCH(1,(CHOOSECOLS(data,1)=ro)*(CHOOSECOLS(data,2)=cf)*(CHOOSECOLS(data,3)=persona),0),
IFERROR(INDEX(data,matchRow,sessionCol+1),"")
)




=LET(
id,$D2,
ro,$A2,
cf,$B2,
persona,$C2,
src,SWITCH(TRUE,
ISNUMBER(SEARCH("POs & PO Conversion",id)),'POs & PO Conversion'!$A$1:$AZ$1000,
ISNUMBER(SEARCH("Payables & Invoicing",id)),'Payables & Invoicing'!$A$1:$AZ$1000,
ISNUMBER(SEARCH("Fieldglass Services SES",id)),'Fieldglass Services SES'!$A$1:$AZ$1000),
sessionCol,XMATCH(id,TAKE(src,1),0),
data,DROP(src,2),
matchRow,XMATCH(1,(CHOOSECOLS(data,1)=ro)*(CHOOSECOLS(data,2)=cf)*(CHOOSECOLS(data,3)=persona),0),
IFERROR(INDEX(data,matchRow,sessionCol+2),"")
)
