# CBT685
Converted to GitHub via [cbt2git](https://github.com/wizardofzos/cbt2git)

This is still a work in progress. 
Due to amazing work by Alison Zhang and Jake Choi repos are no longer deleted.

```
//***FILE 685 is from Pierre Delaunoy and contains a package        *   FILE 685
//*           called TXT2XML, to go from plain text to XML, and     *   FILE 685
//*           also from XML to plain text.                          *   FILE 685
//*                                                                 *   FILE 685
//*          Support email address:                                 *   FILE 685
//*             sunuraxi@users.sourceforge.net                      *   FILE 685
//*                                                                 *   FILE 685
//*          Please submit fix requests                             *   FILE 685
//*          with as much info as possible :-))))                   *   FILE 685
//*                                                                 *   FILE 685
//*          Web site:                                              *   FILE 685
//*          http://sourceforge.net/projects/txt2xml-rexx/          *   FILE 685
//*                                                                 *   FILE 685
//*     Current version:  1.25                                      *   FILE 685
//*                                                                 *   FILE 685
//*     See the change log below:                                   *   FILE 685
//*                                                                 *   FILE 685
//*     TXT2XML                                                     *   FILE 685
//*     =======                                                     *   FILE 685
//*                                                                 *   FILE 685
//*        From TXT (flat files) to XML and vice-versa.             *   FILE 685
//*                                                                 *   FILE 685
//*     1) Introduction                                             *   FILE 685
//*     ---------------                                             *   FILE 685
//*                                                                 *   FILE 685
//*        In 2002, after a XML internet course, I was              *   FILE 685
//*        thoughful. Strange, I thought : XML and COBOL, there     *   FILE 685
//*        are concepts in common. Hierarchy of data, identation    *   FILE 685
//*        for a better visualization, complex entities (in         *   FILE 685
//*        COBOL : group items), ... Wouldn't it be interesting     *   FILE 685
//*        if it was possible to convert data from a flat file      *   FILE 685
//*        to XML one using a COBOL copybook ?                      *   FILE 685
//*                                                                 *   FILE 685
//*        Nobody will stop XML (r)evolution and in my              *   FILE 685
//*        administration, there are plenty of COBOL copybooks      *   FILE 685
//*        and ... flat files So why not ? And in September         *   FILE 685
//*        2002, the first release of TXT2XML was released.         *   FILE 685
//*                                                                 *   FILE 685
//*        "Interesting" say my collegues. But after the            *   FILE 685
//*        migration of all of our programs to the EURO             *   FILE 685
//*        currency, nobody was ready to investigate this           *   FILE 685
//*        technology. There were too much projects that have       *   FILE 685
//*        been delayed ...                                         *   FILE 685
//*                                                                 *   FILE 685
//*        So, TXT2XML was frozen until 2004 when somebody          *   FILE 685
//*        asked me to make conversion in both senses (to and       *   FILE 685
//*        from XML).                                               *   FILE 685
//*                                                                 *   FILE 685
//*     2) Installation                                             *   FILE 685
//*     ---------------                                             *   FILE 685
//*                                                                 *   FILE 685
//*        Very simple :                                            *   FILE 685
//*                                                                 *   FILE 685
//*        a) copy the TXT2XML.PANEL(TXT2XML) to your ISPF          *   FILE 685
//*           panel dataset.                                        *   FILE 685
//*        b) copy the TXT2XML.EXEC(TXT2XML) to your ISPF EXEC      *   FILE 685
//*           or REXX dataset.                                      *   FILE 685
//*        c) copy the TXT2XML.CNTL(TXT2XML) to your JCL            *   FILE 685
//*           DATASET and submit the job. The JCL step names        *   FILE 685
//*           ending with KO should end with a RC = 12 and the      *   FILE 685
//*           JCL step names ending with OK should end with a       *   FILE 685
//*           RC = 0 or 4.                                          *   FILE 685
//*                                                                 *   FILE 685
//*     3) Function / History                                       *   FILE 685
//*     ---------------------                                       *   FILE 685
//*                                                                 *   FILE 685
//*        Function:  Convert a text dataset to of from a XML       *   FILE 685
//*                   one using a COBOL copybook as reference.      *   FILE 685
//*                                                                 *   FILE 685
//*        Invoked from: The ISPF command line (TSO TXT2XML),       *   FILE 685
//*                      another REXX, a batch job.                 *   FILE 685
//*                                                                 *   FILE 685
//*        30/09/02 - Version 0.1                                   *   FILE 685
//*          + start                                                *   FILE 685
//*          + indent XML according to the item level.              *   FILE 685
//*        04/11/02 - Version 0.2                                   *   FILE 685
//*          + handle multi-line cobol item declaration.            *   FILE 685
//*          + ignore line numbers in columns 1-6 & 73-80           *   FILE 685
//*          + ignore level 66, 77, 88 items.                       *   FILE 685
//*          + stop if level is greater than 50.                    *   FILE 685
//*          + stop if level is not numeric.                        *   FILE 685
//*          + stop if some COBOL reserved words are found.         *   FILE 685
//*          + replace 9(4) by 9999 and X(3) by XXX.                *   FILE 685
//*        06/11/02 - Version 0.3                                   *   FILE 685
//*          + handle OCCURS clause for group                       *   FILE 685
//*            and elementary items.                                *   FILE 685
//*        21/11/02 - Version 1.0                                   *   FILE 685
//*          + read line by line instead of reading all  lines.     *   FILE 685
//*          + write line by line instead of writing all lines.     *   FILE 685
//*          + accept any case for COBOL item names.                *   FILE 685
//*        28/06/04 - Version 1.1 RC1                               *   FILE 685
//*          + Bug corrected : VALUES COBOL clauses are now         *   FILE 685
//*            ignored.                                             *   FILE 685
//*          + Make conversion in both senses from XML to           *   FILE 685
//*            TXT and from TXT to XML.                             *   FILE 685
//*          + Renumber cobol levels from 1 by 1 so that            *   FILE 685
//*            identation of XML is independent of absolute         *   FILE 685
//*            COBOL levels.                                        *   FILE 685
//*          + Change input file parameter name to txt and          *   FILE 685
//*            output file parameter name to xml.                   *   FILE 685
//*          + Added a x000 "Records processed" message.            *   FILE 685
//*          + Added a error message if the file transfer           *   FILE 685
//*            of TXT2XML has changed verticals bars                *   FILE 685
//*            (concatenation and OR operator) to |.                *   FILE 685
//*          + Added a report of cobol items: level, name           *   FILE 685
//*            type, start and length .                             *   FILE 685
//*          + During conversion from XML to TXT, check             *   FILE 685
//*            that XML numeric values are really numeric.          *   FILE 685
//*          + Error force termination of the program               *   FILE 685
//*            with return code set to 12.                          *   FILE 685
//*                                                                 *   FILE 685
//*     4) Warnings                                                 *   FILE 685
//*     -----------                                                 *   FILE 685
//*                                                                 *   FILE 685
//*          - You have to parse the XML file with the              *   FILE 685
//*            corresponding DTD, XML schemas.  This REXX will      *   FILE 685
//*            not do any parsing.                                  *   FILE 685
//*          - Attributes of XML elements are ignored.              *   FILE 685
//*          - XML with mixed contents is not supported.            *   FILE 685
//*          - Element content is supposed to be on only one        *   FILE 685
//*            line                                                 *   FILE 685
//*          - Before the conversion from XML to TXT,               *   FILE 685
//*            THE XML INPUT FILE MUST BE "XML WELL-FORMED".        *   FILE 685
//*          - Two ( or more ) dimmension arrays are not            *   FILE 685
//*            supported.                                           *   FILE 685
//*          - level 66, 77, 88 are ignored.                        *   FILE 685
//*          - binary and packed-decimal data are not supported.    *   FILE 685
//*          - Escaping of special characters (&lt; instead of      *   FILE 685
//*            <) is not supported.                                 *   FILE 685
//*          - CDATA is not supported.                              *   FILE 685
//*                                                                 *   FILE 685
//*     5) Todo                                                     *   FILE 685
//*     -------                                                     *   FILE 685
//*                                                                 *   FILE 685
//*          - Support of COBOL binary and packed data ?            *   FILE 685
//*          - Support of attributes of XML elements ?              *   FILE 685
//*          - Support of CDATA                                     *   FILE 685
//*          - Support of escape chars like &lt; for "<"            *   FILE 685
//*          - Support of element content on more than one line     *   FILE 685
//*                                                                 *   FILE 685
```
