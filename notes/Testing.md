Notes from testing algorithms:
===========================
Both algorithms were fooled by the word Computer(computer#n#1), which they both mapped to FinancialService. This is because cash_machine#n#1 is a sibling sense, which mapps to schema:AutomatedTeller, which is the sub-type of FinancialService.
I have attempted a fix, which consists of adding the wn2schema mapping "entity#n#1"->"Thing". This will catch the error in the parent first approach, but will also ensure that far more synsets are mapped to Thing.
This is unfortunate as Thing is the top level entity, and doesn't tell anyting about the thing tagged.
Sadly enough, Thing seems to be the best match for computer in schema.org, unless the computer is being sold, in which case one could use Product or IndividualProduct.

Mapping for verbs might be a little of. I just saw that increase-verb-1 mapps to sumo:FlyingAircraft via hypernym change_magnitude#v#1. This must surly be a mistake, but how can this project be successfull if one cannot trust the mapping files?
synset-explicate-verb-2 maps to sumo:ColdBloodedVertebrate through the parent sibling sense test#v#1 which maps to sumo:Fish, which is a subtype of ColdBloodedVertebrate. Verbs should at least not map to nouns!

Weirdness:
==========
quotation#noun#2 maps to schema MusicRecording, since quotation#noun#2<excerpt#n#1<passage#n#2<section#n#1<music#n#1
It might be that we should stop looking for parents when we get to a hypernym which has two parents, as it is possible that one of these do not maintain the truth value of the synset in question. 
section#n#1 having both music#n#1 and writing#n#1 as hypernymes being a prime example.
It might be better to stop the search and add a default schema:Thing value to the returned JSON instead

tumor#n#1 mapps to OfferItemCondition via growth#n#6<ill_health#n#1<pathological_state#n#1<condition#n#1 which mapps directly to schema:OfferItemCondition. This mapping might be to liberal.
