Notes from testing algorithms:
===========================
Both algorithms were fooled by the word Computer(computer#n#1), which they both mapped to FinancialService. This is because cash_machine#n#1 is a sibling sense, which mapps to schema:AutomatedTeller, which is the sub-type of FinancialService.
I have attempted a fix, which consists of adding the wn2schema mapping "entity#n#1"->"Thing". This will catch the error in the parent first approach, but will also ensure that far more synsets are mapped to Thing.
This is unfortunate as Thing is the top level entity, and doesn't tell anyting about the thing tagged.
Sadly enough, Thing seems to be the best match for computer in schema.org, unless the computer is being sold, in which case one could use Product or IndividualProduct.

Mapping for verbs might be a little of. I just saw that increase-verb-1 mapps to sumo:FlyingAircraft. This must surly be a mistake, but how can this project be successfull if one cannot trust the mapping files?
