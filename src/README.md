# LDD Source Directory

Apollo Mission Dictionary Revisions:

10/15/2021 GEO/SHS
 - Changed definition of Internal_Reference in Metadata_Location, SEED_Equivalent, and ASCII_Equivalent classes, using DD_Association instead of DD_Associate_External_Class. Added rules to validate the reference_type. This is a workaround recommended by Anne Raugh, Small Bodies Node, because LDDTool is currently not correctly handling DD_Associate_External_Class. The original definitions are commented out, and may be restored if LDDTool is revised appropriately.
        
08/05/2022 GEO/JGW 
 - Rebuilt with 1I00 IM


----------

This directory should contain one IngestLDD for the LDD being built.

**The auto-generation script does not currently support multiple versions of an LDD being maintained.**
