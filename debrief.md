# Debrief

## What new insights came out of the discussion?
I like the comparison of SFI to ASLR. That also spawned some 
discussion on the nature of research done in academic versus 
research done in the industry-sphere.

## Was there disagreement? Why?
There was some disagreement about whether dynamic instrumentation 
would be possible given the imprecise nature of dissasembling 
x86/64 binaries. Beyond that, the there wasn't much disagreement 
on the technique itself.

## What was the consensus about the work?
The general consensus was that SFI itself is pretty interesting. 
There were some issues raised, like whether the high-bits based 
technique for segmentation were sufficient for modern applications 
(what if I need to grow my stack/heap outside of the unsafe region, 
or what if I need many unsafe regions).
