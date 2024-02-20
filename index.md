# CSE 15L Lab Report 3: Bugs and Command 

## Part 1: Bugs 

**Associated Code:**

```
public class ArrayExamples {
    // Changes the input array to be in reversed order
    static void reverseInPlace(int[] arr) {
        for(int i = 0; i < arr.length; i += 1) {
            arr[i] = arr[arr.length - i - 1];
        }
    }
}
```

Failure Inducing Input (Test):

```
@Test
public void testReverseInPlace() {
    int[] input1 = {1, 2, 3, 4, 5, 6};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{6, 5, 4, 3, 2, 1}, input1);
}
```

Non Failure-Inducing Input:

```
@Test
public void testReverseOneElementInPlace() {
    int[] input1 = {1};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{1}, input1);
}
```

Symptoms:

```
JUnit version 4.13.2
..E
Time: 0.044
There was 1 failure:
1) testReverseInPlace(ArrayTests)
arrays first differed at element [3]; expected:<3> but was:<4>
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:78)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:28)
        at org.junit.Assert.internalArrayEquals(Assert.java:534)
        at org.junit.Assert.assertArrayEquals(Assert.java:418)
        at org.junit.Assert.assertArrayEquals(Assert.java:429)
        at ArrayTests.testReverseInPlace(ArrayTests.java:11)
        ... 32 trimmed
Caused by: java.lang.AssertionError: expected:<3> but was:<4>
        at org.junit.Assert.fail(Assert.java:89)
        at org.junit.Assert.failNotEquals(Assert.java:835)
        at org.junit.Assert.assertEquals(Assert.java:120)
        at org.junit.Assert.assertEquals(Assert.java:146)
        at org.junit.internal.ExactComparisonCriteria.assertElementsEqual(ExactComparisonCriteria.java:8)
        at org.junit.internal.ComparisonCriteria.arrayEquals(ComparisonCriteria.java:76)
        ... 38 more

FAILURES!!!
Tests run: 2,  Failures: 1
```

Fix the Bug

Before:

```
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
        arr[i] = arr[arr.length - i - 1];
    }
}
```

After:

```
static void reverseInPlace(int[] arr) {
    for (int i = 0; i < arr.length / 2; i += 1) {
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = temp;
    }
}
```
Explanation:
The fix addresses the issue because the value is updated without storing the previous value. Before the temp variable is added and the loop is loop only for half of the array, the ```arr[i] = arr[arr.length - i - 1];``` directly override the value that we need to save it and interchange it. By loop through only half of the array and switch the elements between each other with the value stored in the temp first address the problem that the method change the array value with the wrong way.


## Part 2: Researching Commands

Command Interested ```find```

## ```find -name```

1. First Example

```
nimaikasibatla@Nimais-MacBook-Air technical % find ./plos -name "pmed.001001*"
./plos/pmed.0010010.txt
./plos/pmed.0010013-hepple.xml
./plos/pmed.0010013.txt
./plos/pmed.0010013-s.xml
./plos/pmed.0010013-vp.xml
./plos/pmed.0010013-np.xml
./plos/pmed.0010010-s.xml
./plos/pmed.0010013-logical.xml
./plos/pmed.0010010.anc
./plos/pmed.0010013.anc
./plos/pmed.0010010-np.xml
./plos/pmed.0010010-hepple.xml
./plos/pmed.0010010-vp.xml
./plos/pmed.0010010-logical.xml
```

The ```find -name``` command is returning every path for files that starts with "pmed.001001". This is very useful
if you are trying to find the path of the file where you only know the part of the name.

2. Second Example

```
nimaikasibatla@Nimais-MacBook-Air technical % Find ./government/Env_Prot_Agen -name "*final*"
./government/Env_Prot_Agen/final.txt
./government/Env_Prot_Agen/final-vp.xml
./government/Env_Prot_Agen/final-logical.xml
./government/Env_Prot_Agen/final-np.xml
./government/Env_Prot_Agen/final-hepple.xml
./government/Env_Prot_Agen/final-s.xml
./government/Env_Prot_Agen/final.anc
```
The ```find -name``` command is returning every path for files that contain the string "final" within the file name. Can be used when you know the path of a file
but not the complete file name.

## ```find -type```

1. First Example

```
nimaikasibatla@Nimais-MacBook-Air technical % find ./government -type d
./government
./government/About_LSC
./government/Env_Prot_Agen
./government/Alcohol_Problems
./government/Gen_Account_Office
./government/Post_Rate_Comm
./government/Media
```
The ```find -type``` command is returning the paths for all directories within the path. This is useful if you want the directories paths within a directory rather than the files itself.

2. Second Example

```
nimaikasibatla@Nimais-MacBook-Air technical % find ./plos  -type f -empty
./plos/emptyFile.txt
```
The ```find -type``` command using ```-empty``` Returns the path of any empty file within the directory. Can be used to delete files not being used or empty files.

## ```find -size```

1. First Example

```
nimaikasibatla@Nimais-MacBook-Air technical % find ./government -size +500k
./government/About_LSC/State_Planning_Report-np.xml
./government/About_LSC/Protocol_Regarding_Access-hepple.xml
./government/About_LSC/ONTARIO_LEGAL_AID_SERIES-hepple.xml
./government/About_LSC/State_Planning_Report-vp.xml
./government/About_LSC/LegalServCorp_v_VelazquezDissent-hepple.xml
./government/About_LSC/Strategic_report-hepple.xml
./government/About_LSC/CONFIG_STANDARDS-hepple.xml
./government/About_LSC/commission_report-hepple.xml
./government/About_LSC/diversity_priorities-hepple.xml
./government/About_LSC/reporting_system-hepple.xml
./government/About_LSC/Comments_on_semiannual-hepple.xml
./government/About_LSC/State_Planning_Report-hepple.xml
./government/About_LSC/commission_report-np.xml
./government/About_LSC/LegalServCorp_v_VelazquezOpinion-hepple.xml
./government/About_LSC/Progress_report-hepple.xml
./government/About_LSC/Strategic_report-np.xml
./government/About_LSC/commission_report-vp.xml
./government/About_LSC/conference_highlights-hepple.xml
./government/About_LSC/State_Planning_Special_Report-hepple.xml
./government/About_LSC/Special_report_to_congress-hepple.xml
./government/Env_Prot_Agen/ro_clear_skies_book-hepple.xml
./government/Env_Prot_Agen/tech_adden-hepple.xml
./government/Env_Prot_Agen/tech_adden-vp.xml
./government/Env_Prot_Agen/multi102902-vp.xml
./government/Env_Prot_Agen/atx1-6-np.xml
./government/Env_Prot_Agen/ctm4-10-vp.xml
./government/Env_Prot_Agen/tech_adden-np.xml
./government/Env_Prot_Agen/tech_sectiong-hepple.xml
./government/Env_Prot_Agen/multi102902-np.xml
./government/Env_Prot_Agen/ctm4-10-np.xml
./government/Env_Prot_Agen/ctf7-10-np.xml
./government/Env_Prot_Agen/final-hepple.xml
./government/Env_Prot_Agen/1-3_meth_901-hepple.xml
./government/Env_Prot_Agen/ctf1-6-np.xml
./government/Env_Prot_Agen/nov1-hepple.xml
./government/Env_Prot_Agen/ctf7-10-hepple.xml
./government/Env_Prot_Agen/ctf1-6-hepple.xml
./government/Env_Prot_Agen/section-by-section_summary-np.xml
./government/Env_Prot_Agen/jeffordslieberm-hepple.xml
./government/Env_Prot_Agen/ctm4-10-hepple.xml
./government/Env_Prot_Agen/multi102902-s.xml
./government/Env_Prot_Agen/bill-vp.xml
./government/Env_Prot_Agen/multi102902-hepple.xml
./government/Env_Prot_Agen/section-by-section_summary-hepple.xml
./government/Env_Prot_Agen/jeffordslieberm-np.xml
./government/Env_Prot_Agen/bill-np.xml
./government/Env_Prot_Agen/bill-hepple.xml
./government/Env_Prot_Agen/atx1-6-hepple.xml
./government/Alcohol_Problems/Session3-PDF-hepple.xml
./government/Alcohol_Problems/Session4-PDF-hepple.xml
./government/Alcohol_Problems/Session2-PDF-hepple.xml
./government/Alcohol_Problems/Session3-PDF-vp.xml
./government/Alcohol_Problems/DraftRecom-PDF-hepple.xml
./government/Alcohol_Problems/Session3-PDF-np.xml
./government/Alcohol_Problems/Session4-PDF-np.xml
./government/Alcohol_Problems/Session4-PDF-vp.xml
./government/Gen_Account_Office/Testimony_Jul17-2002_d02957t-hepple.xml
./government/Gen_Account_Office/og97003-hepple.xml
./government/Gen_Account_Office/og96037-hepple.xml
./government/Gen_Account_Office/og97039-hepple.xml
./government/Gen_Account_Office/d01591sp-np.xml
./government/Gen_Account_Office/Testimony_Jul15-2002_d02940t-hepple.xml
./government/Gen_Account_Office/og96011-hepple.xml
./government/Gen_Account_Office/pe1019-s.xml
./government/Gen_Account_Office/og96026-hepple.xml
./government/Gen_Account_Office/d03419sp-np.xml
./government/Gen_Account_Office/July11-2001_gg00172r-hepple.xml
./government/Gen_Account_Office/InternalControl_ai00021p-hepple.xml
./government/Gen_Account_Office/ai2132-hepple.xml
./government/Gen_Account_Office/og96023-hepple.xml
./government/Gen_Account_Office/og96014-hepple.xml
./government/Gen_Account_Office/og97020-hepple.xml
./government/Gen_Account_Office/og96041-hepple.xml
./government/Gen_Account_Office/og96032-hepple.xml
./government/Gen_Account_Office/d01591sp-vp.xml
./government/Gen_Account_Office/ai00134-hepple.xml
./government/Gen_Account_Office/May1998_ai98068-hepple.xml
./government/Gen_Account_Office/og98032-hepple.xml
./government/Gen_Account_Office/Testimony_Jul17-2002_d02957t-np.xml
./government/Gen_Account_Office/ai2132-vp.xml
./government/Gen_Account_Office/d03419sp-hepple.xml
./government/Gen_Account_Office/Oct15-2001_d0224-hepple.xml
./government/Gen_Account_Office/ai9868-hepple.xml
./government/Gen_Account_Office/Testimony_cg00010t-hepple.xml
./government/Gen_Account_Office/pe1019-np.xml
./government/Gen_Account_Office/ai9868-np.xml
./government/Gen_Account_Office/im814-vp.xml
./government/Gen_Account_Office/og96038-hepple.xml
./government/Gen_Account_Office/May1998_ai98068-vp.xml
./government/Gen_Account_Office/d03232sp-np.xml
./government/Gen_Account_Office/ai2132-np.xml
./government/Gen_Account_Office/og96043-hepple.xml
./government/Gen_Account_Office/d03273g-hepple.xml
./government/Gen_Account_Office/gg96118-hepple.xml
./government/Gen_Account_Office/pe1019-vp.xml
./government/Gen_Account_Office/og97051-hepple.xml
./government/Gen_Account_Office/im814-np.xml
./government/Gen_Account_Office/ai9868-vp.xml
./government/Gen_Account_Office/May1998_ai98068-np.xml
./government/Gen_Account_Office/GovernmentAuditingStandards_yb2002ed-np.xml
./government/Gen_Account_Office/d01591sp-hepple.xml
./government/Gen_Account_Office/d01186g-hepple.xml
./government/Gen_Account_Office/Testimony_cg00010t-np.xml
./government/Gen_Account_Office/og97043-hepple.xml
./government/Gen_Account_Office/og96022-hepple.xml
./government/Gen_Account_Office/og96040-hepple.xml
./government/Gen_Account_Office/Sept27-2002_d02966-np.xml
./government/Gen_Account_Office/Oct15-1999_gg00026t-hepple.xml
./government/Gen_Account_Office/d02701-vp.xml
./government/Gen_Account_Office/og97052-hepple.xml
./government/Gen_Account_Office/d01376g-vp.xml
./government/Gen_Account_Office/gg96118-np.xml
./government/Gen_Account_Office/Statements_Feb28-1997_volume-vp.xml
./government/Gen_Account_Office/ai00134-np.xml
./government/Gen_Account_Office/July11-2001_gg00172r-np.xml
./government/Gen_Account_Office/GovernmentAuditingStandards_yb2002ed-vp.xml
./government/Gen_Account_Office/im814-hepple.xml
./government/Gen_Account_Office/og96036-hepple.xml
./government/Gen_Account_Office/Testimony_cg00010t-vp.xml
./government/Gen_Account_Office/d01145g-hepple.xml
./government/Gen_Account_Office/Sept27-2002_d02966-vp.xml
./government/Gen_Account_Office/June30-2000_gg00135r-hepple.xml
./government/Gen_Account_Office/d02701-np.xml
./government/Gen_Account_Office/Sept14-2002_d011070-np.xml
./government/Gen_Account_Office/gg96118-vp.xml
./government/Gen_Account_Office/d01376g-np.xml
./government/Gen_Account_Office/og96027-hepple.xml
./government/Gen_Account_Office/ai00134-vp.xml
./government/Gen_Account_Office/og96045-hepple.xml
./government/Gen_Account_Office/Statements_Feb28-1997_volume-np.xml
./government/Gen_Account_Office/Oct15-2001_d0224-np.xml
./government/Gen_Account_Office/og96020-hepple.xml
./government/Gen_Account_Office/og97041-hepple.xml
./government/Gen_Account_Office/og96042-hepple.xml
./government/Gen_Account_Office/d01376g-hepple.xml
./government/Gen_Account_Office/GovernmentAuditingStandards_yb2002ed-hepple.xml
./government/Gen_Account_Office/og98045-hepple.xml
./government/Gen_Account_Office/Sept14-2002_d011070-hepple.xml
./government/Gen_Account_Office/Testimony_d01609t-hepple.xml
./government/Gen_Account_Office/d0269g-np.xml
./government/Gen_Account_Office/og97032-hepple.xml
./government/Gen_Account_Office/og96031-hepple.xml
./government/Gen_Account_Office/og97050-hepple.xml
./government/Gen_Account_Office/Letter_Walkeraug17let-hepple.xml
./government/Gen_Account_Office/Sept27-2002_d02966-hepple.xml
./government/Gen_Account_Office/ffm-hepple.xml
./government/Gen_Account_Office/d03232sp-hepple.xml
./government/Gen_Account_Office/Statements_Feb28-1997_volume-s.xml
./government/Gen_Account_Office/og96034-hepple.xml
./government/Gen_Account_Office/d01591sp-s.xml
./government/Gen_Account_Office/Paper_Walker11-2002_acpro122-hepple.xml
./government/Gen_Account_Office/og96012-hepple.xml
./government/Gen_Account_Office/d02701-hepple.xml
./government/Gen_Account_Office/og96047-hepple.xml
./government/Gen_Account_Office/og97011-hepple.xml
./government/Gen_Account_Office/pe1019-hepple.xml
./government/Gen_Account_Office/d0269g-vp.xml
./government/Gen_Account_Office/og98022-hepple.xml
./government/Gen_Account_Office/og98040-hepple.xml
./government/Gen_Account_Office/Statements_Feb28-1997_volume-hepple.xml
./government/Post_Rate_Comm/Cohenetal_Scale-hepple.xml
./government/Post_Rate_Comm/Redacted_Study-hepple.xml
./government/Post_Rate_Comm/Cohenetal_comparison-hepple.xml
./government/Post_Rate_Comm/Mitchell_RMVancouver-hepple.xml
./government/Post_Rate_Comm/Mitchell_6-17-Mit-vp.xml
./government/Post_Rate_Comm/Cohenetal_DeliveryCost-hepple.xml
./government/Post_Rate_Comm/Mitchell_6-17-Mit-hepple.xml
./government/Post_Rate_Comm/Mitchell_spyros-first-class-hepple.xml
./government/Post_Rate_Comm/Mitchell_6-17-Mit-np.xml
./government/Post_Rate_Comm/WolakSpeech_usps-hepple.xml
./government/Post_Rate_Comm/Gleiman_EMASpeech-hepple.xml
./government/Post_Rate_Comm/Gleiman_gca2000-hepple.xml
./government/Post_Rate_Comm/Cohenetal_RuralDelivery-hepple.xml
./government/Post_Rate_Comm/Cohenetal_Cost_Function-hepple.xml
./government/Post_Rate_Comm/Cohenetal_CreamSkimming-hepple.xml
./government/Post_Rate_Comm/ReportToCongress2002WEB-hepple.xml
./government/Media/Assuring_Underprivileged-hepple.xml
./government/Media/NJ_Legal_Services-hepple.xml
./government/Media/Poverty_Lawyers-hepple.xml
./government/Media/Law_Schools-hepple.xml
./government/Media/Farm_workers-hepple.xml
./government/Media/Using_Tech_Tools-hepple.xml
./government/Media/Survey-hepple.xml
./government/Media/Coup_Reshapes_Legal_Aid-hepple.xml
./government/Media/Terrorist_Attack-hepple.xml
./government/Media/predatory_loans-hepple.xml
```

The ```find -size``` command is returning the paths for any files in the given directory that have a size more than 500 kilobytes. 
Can help sort large files.

2. Second Example

```
nimaikasibatla@Nimais-MacBook-Air technical % find ./biomed -size +10k -size -11k
./biomed/1471-2334-3-12-logical.xml
./biomed/1471-2164-3-27-logical.xml
./biomed/1476-4598-2-22-logical.xml
./biomed/1471-2091-2-10-logical.xml
./biomed/1471-2474-2-1-logical.xml
./biomed/1471-2210-1-2-logical.xml
./biomed/1471-2458-2-18-logical.xml
./biomed/1471-2407-2-8-logical.xml
./biomed/1471-2377-1-2-logical.xml
./biomed/1472-6920-2-3-logical.xml
./biomed/1471-2180-1-28-logical.xml
./biomed/1472-6947-1-2-logical.xml
./biomed/1471-2431-2-4-logical.xml
./biomed/1475-9268-1-2-logical.xml
./biomed/1471-2156-2-8.txt
./biomed/1471-2164-3-30-logical.xml
./biomed/1472-6890-2-5-logical.xml
./biomed/1471-230X-2-17.txt
./biomed/1471-2350-2-8.txt
```
The ```find -size``` command is returning the paths for any files in a given directory who's size is more than 10 bilobytes but less than 11 kilobytes. Can find files
with certain size ranges.

### ```find - delete```

1. First Example

```
nimaikasibatla@Nimais-MacBook-Air technical % find ./biomed  -name "1471*" -delete 
nimaikasibatla@Nimais-MacBook-Air technical %
```
The ```find -delete``` command removed every file in the given directory starting with 1471. Can be useful for deleting files you know the directory and name of. 

2. Second Example

```
nimaikasibatla@Nimais-MacBook-Air technical % find ./government -type f -delete
nimaikasibatla@Nimais-MacBook-Air technical %
```
The ```find -delete``` command is used to remove every file in the given path government. Can be used to delete all the files within a given directory.


