# Christopher Schrader - Lab Report 3

# Part 1
For part 1, I have chosen the faulty `reverseInPlace()` function from `ArrayExamples.java`

## Failure inducing input using `{3, 5, 2}` as my array:

```
 @Test
  public void testReverseInPlaceTwo() {
    int[] input1 = { 3, 5, 2 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{2, 5, 3 }, input1);
  }
```

## Input that doesn't produce a failure using `{3}` as my array:

```
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```

## Symptom:
![Symptom output](labreport_1.png)

## The bug:
The bug was that in the old code, the values of the array were being overwritten as the array was reversed. For example, when the last element was swapped with the first element, the first element was lost forever. I fixed the bug by keeping a temporary `int temp` variable that stores the value of the element at `arr[i]` so that we do not lose it and can put it at the corresponding opposite side of the array. We only loop up to the middle ement since once we get to that point the array has been successfully reversed.

Before code change:
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

After code change:
```
  static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length / 2; i += 1) {
      int temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```
# Part 2
For part 2, I've chosen the `grep` command.

My first option is using the `-C n` option, which gives context by printing n lines before and after the line where the pattern is found.
I found this option through the `man` command.
Example 1:
```
christopherschrader@Christophers-MacBook-Pro-2 docsearch % grep -C 1 "cancer" ./technical/biomed/gb-2003-4-7-r46.txt
        plays a critical part in its development. However,
        investigations into the molecular biology of cancers are
        often carried out on cells grown 
--
        in vivo tissue environment in which
        cancers naturally develop. The effects of these
        environmental differences on cancer cells may account, in
        part, for the fact that only a small percentage of
        anticancer drugs that are found to effectively kill cells 
        in vitro are successful in subsequent
--
        in one cell line but not the other.
        In modeling mechanisms of cancer development, global
        gene-expression profiling of human-derived cells grown as
--
        different patients, lesser genetic heterogeneity would be
        expected in xenografts of cancer cells originally derived
        from a single patient. Furthermore, patient-derived tumors
        are composed of both cancer and non-cancer cells, making it
        difficult to precisely ascertain gene-expression patterns
        specifically attributable to cancer cells. For example, in
        many cancer microarray studies, the actual percentage of
        cancer cells in a profiled sample may be as low as 30-40% [
        2 ] . Even when using techniques such as laser capture
        microdissection, which can improve tumor purity [ 3 ] , the
        relative contribution of cancer cells and non-cancer cells
        to the overall gene-expression profile remains uncertain.
--
        xenograft using a human microarray chip might uncover genes
        specifically expressed in human cancer cells in xenograft
        tumors comprised of a mixture of human- and mouse-derived
--
          changes observed in gene expression in the xenograft
          tumors are due to the cancerous (human) cells and not the
          surrounding (mouse) host tissue.
--
          Overrepresentation of genes involved in cell
          division and metabolism among genes upregulated in cancer
          cells in culture relative to xenografts
--
          adhesion, the extracellular matrix, and vascularization
          among genes upregulated in cancer cells in xenografts
          relative to cultures
--
          preexisting vessels for the delivery of nutrients to
          tumors. Other disease-related terms include 'Precancerous
          conditions' (11,8), 'Pulmonary fibrosis' (5,5; a
--
          cells' (23,20), as similar signaling pathways are thought
          to regulate self-renewal in stem cells and cancer cells,
          and as tumors may include stem cells [ 9 ] . The entire
--
          Whereas processes of cell division and metabolism may be
          more in common from one cancer to the next, processes of
          cell adhesion and ECM interaction are likely to be very
--
          observations gave rise to the hypothesis that, when
          placed in comparable tissue environments, cancer cells
          from different lineages may express different cell
--
        oxygen and are subjected to or benefit from a wide variety
        of host factors. The ability of cancer cells to proliferate
        within a tissue depends on their response to adhesive and
--
        self-sufficiency in growth signals is one of the hallmarks
        of cancer [ 11 ] . To stimulate their own growth and
        proliferation in tissue, tumor cells can overproduce and
--
        in vivo tumor.
        In terms of new biological insight into cancer
        development, our findings suggest that cancer cells of
        different origins interact in different ways with the same
--
        environment is different from the tissue of origin of the
        cancer. This conclusion is based on the significant
        representation of genes associated with cell adhesion and
--
        in the xenografts, assessment of the specific contribution
        of cancer cells to the increased expression may be
        difficult. In the case of human tumor xenografts in a mouse
--
        expression of cell adhesion and ECM genes is upregulated in
        the cancerous cells in the tumor tissue. This conclusion is
        based on the following two observations. First, profiling
--
        The findings presented here, suggesting that different
        ECM signaling pathways are active in different cancers,
        could have important clinical implications, as knowledge of
        the specific pathways dysregulated in a particular cancer
        may be valuable for devising effective therapy that targets
--
        have identified genes that appear upregulated in certain
        cancers 
        in vivo compared to 
--
        interest are genes that are upregulated in both the
        cancers, including 
        IGFBP3 (insulin-like growth factor
```
This command prints out every line in `/technical/biomed/gb-2003-4-7-r46.txt` that contains "cancer" as well as one line below and above it. This is useful as it provides context every time cancer is mentioned.

Example 2:
```
hristopherschrader@Christophers-MacBook-Pro-2 docsearch % grep -C 1 "base pair" ./technical/plos/*.txt 
./technical/plos/journal.pbio.0020190.txt-        DNA generally? Or does it happen to particular sequences? Bacteria have their chi (χ)
./technical/plos/journal.pbio.0020190.txt:        sequence, which is a specific series of eight base pairs in the DNA of the bacterial
./technical/plos/journal.pbio.0020190.txt-        chromosome that stimulate the action of proteins that bring about recombination (Eggleston
--
./technical/plos/journal.pbio.0020190.txt-        occur than in other places on the chromosome. Recombination hotspots are local regions of
./technical/plos/journal.pbio.0020190.txt:        chromosomes, on the order of one or two thousand base pairs of DNA (or less—their length is
./technical/plos/journal.pbio.0020190.txt-        difficult to measure), in which recombination events tend to be concentrated. Often they
--
./technical/plos/journal.pbio.0020223.txt-        with reagents that are covalently linked to complementary DNA oligonucleotides. Upon
./technical/plos/journal.pbio.0020223.txt:        Watson-Crick base pairing, the proximity of the synthetic reactive groups elevates their
./technical/plos/journal.pbio.0020223.txt-        effective molarity by several orders of magnitude, inducing a chemical reaction. Because
```
This command prints out every line in .txt files in technical/plos/ plus one line above and below it for context that has the phrase "base pair." This is useful since earlier we saw there were 3 matches for it but we had no context.

My second option is the -o option, which specifies that it only prints the part of the line that matches the pattern.

Example 1:
```
christopherschrader@Christophers-MacBook-Pro-2 docsearch % grep -o "base case" ./technical/plos/*.txt
./technical/plos/pmed.0020016.txt:base case
```
Here, we print out the exact pattern match for every .txt file in technical/plos for the pattern "base case." This is useful if we only care about the actual pattern match without context.

Example 2:
```
christopherschrader@Christophers-MacBook-Pro-2 docsearch % grep -o "cancer" ./technical/plos/*.txt
./technical/plos/journal.pbio.0020013.txt:cancer
./technical/plos/journal.pbio.0020028.txt:cancer
./technical/plos/journal.pbio.0020028.txt:cancer
./technical/plos/journal.pbio.0020028.txt:cancer
./technical/plos/journal.pbio.0020028.txt:cancer
./technical/plos/journal.pbio.0020028.txt:cancer
./technical/plos/journal.pbio.0020035.txt:cancer
./technical/plos/journal.pbio.0020035.txt:cancer
./technical/plos/journal.pbio.0020040.txt:cancer
./technical/plos/journal.pbio.0020040.txt:cancer
./technical/plos/journal.pbio.0020040.txt:cancer
./technical/plos/journal.pbio.0020040.txt:cancer
./technical/plos/journal.pbio.0020040.txt:cancer
./technical/plos/journal.pbio.0020040.txt:cancer
./technical/plos/journal.pbio.0020040.txt:cancer
./technical/plos/journal.pbio.0020040.txt:cancer
./technical/plos/journal.pbio.0020040.txt:cancer
./technical/plos/journal.pbio.0020052.txt:cancer
./technical/plos/journal.pbio.0020053.txt:cancer
./technical/plos/journal.pbio.0020053.txt:cancer
./technical/plos/journal.pbio.0020063.txt:cancer
./technical/plos/journal.pbio.0020071.txt:cancer
./technical/plos/journal.pbio.0020112.txt:cancer
./technical/plos/journal.pbio.0020113.txt:cancer
./technical/plos/journal.pbio.0020148.txt:cancer
./technical/plos/journal.pbio.0020148.txt:cancer
./technical/plos/journal.pbio.0020148.txt:cancer
./technical/plos/journal.pbio.0020148.txt:cancer
./technical/plos/journal.pbio.0020148.txt:cancer
./technical/plos/journal.pbio.0020169.txt:cancer
./technical/plos/journal.pbio.0020347.txt:cancer
./technical/plos/journal.pbio.0020400.txt:cancer
./technical/plos/journal.pbio.0020404.txt:cancer
./technical/plos/journal.pbio.0020419.txt:cancer
./technical/plos/journal.pbio.0020419.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0020439.txt:cancer
./technical/plos/journal.pbio.0030094.txt:cancer
./technical/plos/pmed.0010008.txt:cancer
./technical/plos/pmed.0010008.txt:cancer
./technical/plos/pmed.0010008.txt:cancer
./technical/plos/pmed.0010026.txt:cancer
./technical/plos/pmed.0010026.txt:cancer
./technical/plos/pmed.0010026.txt:cancer
./technical/plos/pmed.0010026.txt:cancer
./technical/plos/pmed.0010026.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010028.txt:cancer
./technical/plos/pmed.0010050.txt:cancer
./technical/plos/pmed.0010050.txt:cancer
./technical/plos/pmed.0010050.txt:cancer
./technical/plos/pmed.0010050.txt:cancer
./technical/plos/pmed.0010050.txt:cancer
./technical/plos/pmed.0010052.txt:cancer
./technical/plos/pmed.0010052.txt:cancer
./technical/plos/pmed.0010052.txt:cancer
./technical/plos/pmed.0010060.txt:cancer
./technical/plos/pmed.0010062.txt:cancer
./technical/plos/pmed.0010064.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010066.txt:cancer
./technical/plos/pmed.0010067.txt:cancer
./technical/plos/pmed.0010067.txt:cancer
./technical/plos/pmed.0010067.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0010069.txt:cancer
./technical/plos/pmed.0020007.txt:cancer
./technical/plos/pmed.0020017.txt:cancer
./technical/plos/pmed.0020017.txt:cancer
./technical/plos/pmed.0020017.txt:cancer
./technical/plos/pmed.0020017.txt:cancer
./technical/plos/pmed.0020017.txt:cancer
./technical/plos/pmed.0020021.txt:cancer
./technical/plos/pmed.0020021.txt:cancer
./technical/plos/pmed.0020021.txt:cancer
./technical/plos/pmed.0020021.txt:cancer
./technical/plos/pmed.0020021.txt:cancer
./technical/plos/pmed.0020021.txt:cancer
./technical/plos/pmed.0020033.txt:cancer
./technical/plos/pmed.0020034.txt:cancer
./technical/plos/pmed.0020055.txt:cancer
./technical/plos/pmed.0020059.txt:cancer
./technical/plos/pmed.0020059.txt:cancer
./technical/plos/pmed.0020062.txt:cancer
./technical/plos/pmed.0020062.txt:cancer
./technical/plos/pmed.0020062.txt:cancer
./technical/plos/pmed.0020062.txt:cancer
./technical/plos/pmed.0020073.txt:cancer
./technical/plos/pmed.0020073.txt:cancer
./technical/plos/pmed.0020073.txt:cancer
./technical/plos/pmed.0020073.txt:cancer
./technical/plos/pmed.0020073.txt:cancer
./technical/plos/pmed.0020073.txt:cancer
./technical/plos/pmed.0020073.txt:cancer
./technical/plos/pmed.0020073.txt:cancer
./technical/plos/pmed.0020074.txt:cancer
./technical/plos/pmed.0020074.txt:cancer
./technical/plos/pmed.0020074.txt:cancer
./technical/plos/pmed.0020074.txt:cancer
./technical/plos/pmed.0020074.txt:cancer
./technical/plos/pmed.0020074.txt:cancer
./technical/plos/pmed.0020074.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020075.txt:cancer
./technical/plos/pmed.0020091.txt:cancer
./technical/plos/pmed.0020160.txt:cancer
./technical/plos/pmed.0020181.txt:cancer
./technical/plos/pmed.0020210.txt:cancer
./technical/plos/pmed.0020237.txt:cancer
./technical/plos/pmed.0020237.txt:cancer
./technical/plos/pmed.0020272.txt:cancer
./technical/plos/pmed.0020272.txt:cancer
./technical/plos/pmed.0020273.txt:cancer
./technical/plos/pmed.0020275.txt:cancer
```
This prints out the matches for every .txt file in /technical/plos using the pattern "cancer." This can be useful if we're trying to find technical studies on cancer.

My third command option is `-c` which prints out the number of times a pattern is matched in a given file.
I found this option in the following source: [source](https://www.thegeekstuff.com/2009/03/15-practical-unix-grep-command-examples/)

Example 1:
```
christopherschrader@Christophers-MacBook-Pro-2 docsearch % grep -c "author" ./technical/plos/pmed.0020201.txt
5
```
This command prints out how many times "author" is matched in `pmed.0020201.txt`

Example 2:
```
christopherschrader@Christophers-MacBook-Pro-2 docsearch % grep -c "rRNA" ./technical/biomed/gb-2003-4-2-r14.txt
6
```
This command prints out how many times "rRNA" is matched in `gb-2003-4-2-r14.txt`, which can be useful if we're trying to see if the article talks about rRNA a lot.

The fourth and final command option is `-n`, which includes the line number the pattern is matched.
I found this at the following source: [source](https://www.linuxandubuntu.com/home/how-to-make-good-use-of-grep-command)

Example 1:
```
hristopherschrader@Christophers-MacBook-Pro-2 docsearch % grep -n "rRNA" ./technical/biomed/gb-2003-4-2-r14.txt
30:          Woese [ 16] contends that the rRNA tree is a valid
104:          spaced from one another on the 16S rRNA tree.
550:          16S rRNA tree, although the 
798:          Figure 9shows a segment of the 16S rRNA tree that
843:          trp-pathway genes in the 16S rRNA tree sector that is
1181:          16S rRNA subtrees were derived from the Ribosomal
```
This printed out the line and line number where "rRNA" was matched in the given file. This is useful so we can refer to the line number in the file to see what they're saying about rRNA.

Example 2:
```
christopherschrader@Christophers-MacBook-Pro-2 docsearch % grep -n "author" ./technical/plos/*.txt
./technical/plos/journal.pbio.0020001.txt:130:        a region with a publication if any of the authors were affiliated with institutions from
./technical/plos/journal.pbio.0020001.txt:132:        that publication had been written by multiple authors from institutions of different
./technical/plos/journal.pbio.0020001.txt:163:        ecology and environmental sciences emphasizes the overwhelming contributions of authors
./technical/plos/journal.pbio.0020010.txt:23:        subscription-based and open-access publishers improve their services to authors and to
./technical/plos/journal.pbio.0020010.txt:53:        knowledge is essential in ‘selling’ their services to authors. The globalisation of
./technical/plos/journal.pbio.0020035.txt:131:        In the first paper (Tang et al. 2003), the authors explore the hypothesis that the CLF
./technical/plos/journal.pbio.0020035.txt:138:        length of the product increased as expected. The authors propose that the length of the
./technical/plos/journal.pbio.0020040.txt:45:        Next, the authors did a rigorous test of different functions of the p53 protein. They
./technical/plos/journal.pbio.0020040.txt:60:        irradiation-induced DNA damage. The authors studied the expression of two p53-upregulated
./technical/plos/journal.pbio.0020046.txt:153:        authors concluded that the primary dysfunction is located in the left hemisphere and that
./technical/plos/journal.pbio.0020047.txt:23:        knowledge—the workings of the brain and the nature of creativity. Its author, a neurologist
./technical/plos/journal.pbio.0020047.txt:30:        disconcerting blend of pop-science and pop-confessional genres. The author frequently talks
./technical/plos/journal.pbio.0020047.txt:35:        Given that the book topic is promising and that the author can often write very well, it
./technical/plos/journal.pbio.0020047.txt:60:        on these questions. Its focus is the domain of writing, drawing from the author's own
./technical/plos/journal.pbio.0020053.txt:11:        according to the senior author on that paper, Marc Lipsitch. But no one doubts that
./technical/plos/journal.pbio.0020064.txt:93:        another unknown receptor’, says lead author Sami Damak (Mount Sinai School of Medicine, New
./technical/plos/journal.pbio.0020067.txt:92:        him to be a coauthor of the paper. Wilkins, true to his character, declined, as he had not
./technical/plos/journal.pbio.0020067.txt:113:        failure. Riddled by secrecy, diffuse lines of authority, the absence of strategies, and a
./technical/plos/journal.pbio.0020071.txt:17:        that the authors draw on a range of carefully chosen human traits to illustrate their
./technical/plos/journal.pbio.0020071.txt:23:        function, the authors discuss the relatively poor sense of smell in humans, as compared
./technical/plos/journal.pbio.0020071.txt:38:        In Chapter 7, the authors discuss five topics that have traditionally been hard to
./technical/plos/journal.pbio.0020073.txt:63:        biotinylated tiles, with each biotin moiety separated by about 19 nm. The authors then
./technical/plos/journal.pbio.0020100.txt:11:        emerge in a paper written by Baum and Perrimon (2001), in which the authors showed the
./technical/plos/journal.pbio.0020100.txt:37:        the authors identified new functional roles for actin regulators such as CAP (a 
./technical/plos/journal.pbio.0020100.txt:47:        in mammalian cells, were found to work with CAP in this process. The authors proposed that
./technical/plos/journal.pbio.0020100.txt:78:        in the formation of lamellae. The authors looked at the effects of loss of function in 90
./technical/plos/journal.pbio.0020105.txt:19:        the publication-charge model puts an unfair burden on authors. Subsequently, we will
./technical/plos/journal.pbio.0020105.txt:26:        By charging authors a fee to have their work published in lieu of charging readers to
./technical/plos/journal.pbio.0020105.txt:29:        seemingly untested revenue stream has generated skepticism that authors will be both
./technical/plos/journal.pbio.0020105.txt:31:        Publication fees are not a phenomenon born of the open-access movement. Many authors
./technical/plos/journal.pbio.0020105.txt:35:        EMBO Journal , for example, authors are allowed six pages of text free,
./technical/plos/journal.pbio.0020105.txt:37:        all authors exceed six pages, voluntarily paying on average over $800 to publish their
./technical/plos/journal.pbio.0020105.txt:39:        Furthermore, in addition to paying other publication charges, authors may be willing to
./technical/plos/journal.pbio.0020105.txt:41:        recognized. A recent survey of authors in the 
./technical/plos/journal.pbio.0020105.txt:46:        PNAS authors expressed a willingness to pay an “open-access surcharge” of
./technical/plos/journal.pbio.0020105.txt:49:        PNAS author already pays (Cozzarelli et al. 2004).
./technical/plos/journal.pbio.0020105.txt:50:        Although we recognize that authors who submit to 
./technical/plos/journal.pbio.0020105.txt:55:        The concern about authors' ability to pay publication charges will become less pressing
./technical/plos/journal.pbio.0020105.txt:65:        reduce authors' reliance on individual grants to support charges directly and ensure equal
./technical/plos/journal.pbio.0020105.txt:71:        open-access publishing may lead to a situation in which some authors are simply unable to
./technical/plos/journal.pbio.0020105.txt:73:        of authors to pay publication charges must never be a consideration in the decision to
./technical/plos/journal.pbio.0020105.txt:75:        neither the editors nor the reviewers know which authors have indicated whether or not they
./technical/plos/journal.pbio.0020105.txt:78:        publishers have always absorbed some authors' inability to pay page and color charges. PLoS
./technical/plos/journal.pbio.0020105.txt:79:        grants full or partial publication-charge waivers to any author who requests them, no
./technical/plos/journal.pbio.0020105.txt:87:        open-access publication charges for authors who cannot afford them. The Open Society
./technical/plos/journal.pbio.0020105.txt:90:        Membership that grants waived publication charges to authors while providing compensatory
./technical/plos/journal.pbio.0020105.txt:93:        authors resides in the terminology—the term “author charge” is itself misleading.
./technical/plos/journal.pbio.0020105.txt:94:        Publication fees are not borne purely by authors, but are shared by the many organizations
./technical/plos/journal.pbio.0020105.txt:97:        intermediaries between authors and journals, as OSI does. Others—including many
./technical/plos/journal.pbio.0020112.txt:63:        authoritative and blow-by-blow account shows failings not only in the butcher (who was,
./technical/plos/journal.pbio.0020113.txt:234:        coastal state boundaries and authorities. The Sea Grant program in conjunction with
./technical/plos/journal.pbio.0020121.txt:17:        authorities haven't ruled out the possibility of a public health threat. The media have
./technical/plos/journal.pbio.0020125.txt:166:        PLoS Biology by Osherovich et al. (2004), the authors examined sequence
./technical/plos/journal.pbio.0020125.txt:175:        inheritance. The authors suggested that the oligopeptide repeats facilitate the division of
./technical/plos/journal.pbio.0020125.txt:180:        authors constructed an F chimera, a fusion protein having the N-rich domain of New1 and the
./technical/plos/journal.pbio.0020127.txt:31:        al. 2004) and, of course, because of the experience of this author. Here I shall outline
./technical/plos/journal.pbio.0020127.txt:130:        Xenopus and the factors involved in this process. The authors
./technical/plos/journal.pbio.0020140.txt:36:        important results. The authors lesioned discrete parts of the prefrontal cortex in
./technical/plos/journal.pbio.0020145.txt:42:        the data rather than the authors': this is a very substantial improvement in student
./technical/plos/journal.pbio.0020145.txt:167:        authors (Brill and Yarden 2003). Students quickly figure out what intellectual behaviors
./technical/plos/journal.pbio.0020147.txt:7:        Princeton University Press, is a work of advocacy in which the authors argue that
./technical/plos/journal.pbio.0020147.txt:12:        environment in which it is subject to natural selection. The authors' major assertion is
./technical/plos/journal.pbio.0020147.txt:32:        After this broad, accessible survey, the authors change key rather abruptly and explore
./technical/plos/journal.pbio.0020147.txt:45:        thermodynamics and Maxwell's Demon, the authors lead us through a challenging thesis that
./technical/plos/journal.pbio.0020147.txt:54:        successful part. Though it is rare for the authors to offer new analysis and insight, their
./technical/plos/journal.pbio.0020147.txt:68:        succession. It is a great pity that the authors give so little space to plants and plant
./technical/plos/journal.pbio.0020147.txt:85:        for the biological and human sciences to integrate across subdisciplines, as the authors
./technical/plos/journal.pbio.0020156.txt:76:        author charges and other means,” John Hawley, the executive director of the ASCI writes,
./technical/plos/journal.pbio.0020156.txt:78:        JCI hopefully can bring the greatest benefit to its authors and readers,
./technical/plos/journal.pbio.0020156.txt:83:        Physiological Society, for example, offers authors in 
./technical/plos/journal.pbio.0020156.txt:86:        Joint Information Systems Committee (JISC) in the United Kingdom suggests that many authors
./technical/plos/journal.pbio.0020156.txt:87:        would use such an option if it were more widely available: 48% of authors who had never
./technical/plos/journal.pbio.0020156.txt:88:        published in an open-access journal and 60% of authors who had done so indicated that they
./technical/plos/journal.pbio.0020156.txt:90:        subscription model an additional fee for them to make [the author's] particular paper ‘open
./technical/plos/journal.pbio.0020156.txt:94:        providing grants to offset the publication charges for authors during this transitional
./technical/plos/journal.pbio.0020164.txt:135:        Indeed, the major message of the von Dassow article was that the authors had uncovered a
./technical/plos/journal.pbio.0020169.txt:118:        one another, the authors defined a specific transmembrane domain interface in resting α
./technical/plos/journal.pbio.0020187.txt:23:        short commentary by another distinguished author. Within their own scope, all of these
./technical/plos/journal.pbio.0020213.txt:233:        hybridisation is not known,’ note the authors of a DEFRA report on the mystery species
./technical/plos/journal.pbio.0020214.txt:30:        authority to distribute money (Figure 1). The funds come both as long-term support for
./technical/plos/journal.pbio.0020214.txt:129:        at authors' Web pages, and last but not least, colleagues abroad who break copyright laws
./technical/plos/journal.pbio.0020215.txt:56:        Aiming to investigate how TNTs were linking cells, the authors performed scanning and
./technical/plos/journal.pbio.0020224.txt:95:        the silencing signal. The authors also found that antisense-induced silencing was never
./technical/plos/journal.pbio.0020228.txt:23:        In practice, academic authors typically assign full copyrights to their articles to the
./technical/plos/journal.pbio.0020228.txt:36:        copyright holders to prevent some uses of a work without permission, but to authorize
./technical/plos/journal.pbio.0020228.txt:40:        License) or for any purpose at all provided that the original authorship is properly
./technical/plos/journal.pbio.0020228.txt:68:        be included in coursepacks—a use-right that most authors would want to allow without
./technical/plos/journal.pbio.0020228.txt:70:        they rarely share with authors). The CCAL also ensures that institutions are permitted to
./technical/plos/journal.pbio.0020228.txt:84:        any use that any entrepreneur can envision, so long as the authors of the papers are
./technical/plos/journal.pbio.0020228.txt:96:        articles that authors would object to—while the CCAL permits such uses and renders authors
./technical/plos/journal.pbio.0020228.txt:110:        has published, we are loath to prevent an author's work from wider distribution. Any risk
./technical/plos/journal.pbio.0020228.txt:111:        that a company will use an article for a purpose its author would be uncomfortable with is,
./technical/plos/journal.pbio.0020228.txt:118:        authors are inappropriate copyright holders because they are ill-equipped to protect their
./technical/plos/journal.pbio.0020228.txt:127:        articles authors would actually want to prevent (other than, perhaps, the commercial uses
./technical/plos/journal.pbio.0020228.txt:133:        Those applications, however, tend not to constitute “misuse” in many authors' eyes.
./technical/plos/journal.pbio.0020228.txt:139:        radical understanding of the interests of authors and users of primary research articles to
./technical/plos/journal.pbio.0020228.txt:143:        similar legal arrangements with authors as a matter of course? One answer is to “vote with
./technical/plos/journal.pbio.0020228.txt:144:        your submissions;” that is, authors should submit their work preferentially to journals
./technical/plos/journal.pbio.0020228.txt:156:        and build upon it. When authors publish their work in journals with restrictive copyright
./technical/plos/journal.pbio.0020228.txt:157:        practices, it becomes illegal (often for even the authors themselves) to store primary
./technical/plos/journal.pbio.0020263.txt:15:        Whose genes will be studied? For what purpose? And who has the authority to decide?
./technical/plos/journal.pbio.0020346.txt:59:        authors try to provide alternatives to innate predispositions, such as the importance of
./technical/plos/journal.pbio.0020401.txt:57:        protein aggregates are referred to as oligomers or protofibrils. Some authors have argued
./technical/plos/journal.pbio.0020420.txt:40:        selection against hybrids, is reinforcement sensu Dobzhansky (1937). Recent authors have
./technical/plos/journal.pbio.0020420.txt:119:        this approach. Using high-resolution genetic mapping the authors have identified the
./technical/plos/journal.pbio.0020440.txt:105:        correct.” Kozlowski is the co-author of a theory that relates metabolic rate to cell size
./technical/plos/journal.pbio.0020440.txt:115:        The metabolic theory's authors are not budging. “We've yet to see a criticism we feel we
./technical/plos/journal.pbio.0030021.txt:166:        C. briggsae . The authors also identify a short, C-terminal
./technical/plos/journal.pbio.0030032.txt:127:        author of the forthcoming book 
./technical/plos/journal.pbio.0030056.txt:84:        with the much larger short-faced bears, the authors argue (Figure 2).
./technical/plos/journal.pbio.0030056.txt:133:        first author of the salt-crystal study, is adamant that his methods were exacting. “The
./technical/plos/journal.pbio.0030056.txt:155:        criteria are used by authors and referees as a checklist, he says. This does not mean the
./technical/plos/journal.pbio.0030056.txt:157:        But allowing authors the freedom to use the criteria as they see fit could come at a
./technical/plos/journal.pbio.0030062.txt:6:        Despite the biases that a single author inevitably brings to a subject, only one or a
./technical/plos/journal.pbio.0030062.txt:7:        few closely interacting authors can bring coherence, synthesis, and vision to a broad and
./technical/plos/journal.pbio.0030062.txt:13:        species concepts, it has been 23 years since Verne Grant's authoritative 
./technical/plos/journal.pbio.0030062.txt:148:        topics, and undoubtedly will remain so despite the careful analyses by these authors. They
./technical/plos/journal.pbio.0030065.txt:10:        published in peer-reviewed journals. As part of the publication process, some authors
./technical/plos/journal.pbio.0030065.txt:55:        call the authors to iron out any ambiguities. Curators can also cope with the high
./technical/plos/journal.pbio.0030065.txt:106:        database (perhaps because of an author error, or an alternative name for an entity adopted
./technical/plos/journal.pbio.0030065.txt:143:        tags during submission, which have to be verified by the author. Text mining is ready to
./technical/plos/journal.pbio.0030065.txt:144:        deliver tools whereby information is passed back to the authors about the proper use of
./technical/plos/journal.pbio.0030065.txt:146:        if the use of a term is wrong, the author is asked to provide feedback. The curation effort
./technical/plos/journal.pbio.0030065.txt:150:        article. Publishers and authors have to agree on standards though.
./technical/plos/journal.pbio.0030065.txt:171:        methods improve, authors will see more and more of their text being analysed and formalised
./technical/plos/journal.pbio.0030065.txt:172:        in a database. If appropriate quality control is provided, and if authors receive due
./technical/plos/journal.pbio.0030097.txt:49:        [2]. Essentially, the producers (researchers as authors) and the consumers (researchers as
./technical/plos/journal.pbio.0030097.txt:56:        to the author (the researcher who wrote the piece) or even to the consulting experts (the
./technical/plos/journal.pbio.0030097.txt:102:        an author-side payment model is estimated as US$1,950—a comparable saving of 30% on the
./technical/plos/journal.pbio.0030102.txt:115:        special function in the energy cycle of the organism—as in plant roots. Several authors
./technical/plos/journal.pbio.0030129.txt:20:        The PLoS community journals will give authors an opportunity to publish a greater range
./technical/plos/journal.pbio.0030129.txt:65:        confidentiality. That said, if an author would like a manuscript that has been turned down
./technical/plos/journal.pbio.0030129.txt:68:        help to expedite the review process, saving time for authors, editors, and reviewers. The
./technical/plos/journal.pbio.0030131.txt:21:        In this study, the authors use a differential isolation procedure to remove the skeletal
./technical/plos/journal.pbio.0030131.txt:95:        field. In addition, the authors go on to show the acquisition of the differentiated cardiac
./technical/plos/pmed.0010013.txt:27:        tolerance to foreign donor cells. In all three cases, the authors' work led to powerful
./technical/plos/pmed.0010021.txt:116:          gradual improvement occurred [14]. Strangely, the authors concluded that large doses were
./technical/plos/pmed.0010021.txt:141:        response of patients to any dose is variable. Some authors have suggested that this may be
./technical/plos/pmed.0010022.txt:18:        put articles into books—just give the author proper credit).
./technical/plos/pmed.0010022.txt:72:        require authors to tell us of any possible competing interests; we in turn will tell
./technical/plos/pmed.0010023.txt:39:        also seen in two of the patients who were clinically tolerant to oats. The authors suggest
./technical/plos/pmed.0010024.txt:37:        children, what should people who treat children with malaria do? The authors' first
./technical/plos/pmed.0010025.txt:29:        authors, indicate that Th1 cells, but not Th2 cells, are required for producing the
./technical/plos/pmed.0010026.txt:61:        authors propose that the cause for the decreased affinity of vaccine-elicited CTLs could be
./technical/plos/pmed.0010030.txt:36:        authors clearly state that the company had “a nonbinding input on issues of study design
./technical/plos/pmed.0010046.txt:17:        reject it just because the authors failed to systematically review the literature when
./technical/plos/pmed.0010050.txt:36:        The authors suggest that the high doses of peptides administered in vaccinations and the
./technical/plos/pmed.0010052.txt:113:        for Robert Wilson, the gynecologist and author of the best-selling book 
./technical/plos/pmed.0010052.txt:181:        authors?
./technical/plos/pmed.0010060.txt:17:        registry authorized by the Food and Drug Modernization Act of 1997, appears not to be
./technical/plos/pmed.0010064.txt:53:          Health and Human Services and of the authors' institutions were followed. The study
./technical/plos/pmed.0010067.txt:27:        The authors developed the algorithm in a training group of 36 patients and then
./technical/plos/pmed.0010069.txt:36:        with 32,000 cancer cases) and the high quality of data enables the authors to detect subtle
./technical/plos/pmed.0010070.txt:37:        function in the STI group, the authors conclude that, in light of the possibility of
./technical/plos/pmed.0010070.txt:40:        resistant mutants should be of concern. The authors point out that all participants were
./technical/plos/pmed.0010071.txt:31:        authority.
./technical/plos/pmed.0020005.txt:40:        authors argue that these large scales are necessary to eliminate “idiosyncratic”
./technical/plos/pmed.0020009.txt:60:        the authority to provide real oversight.
./technical/plos/pmed.0020020.txt:46:        for further vaccine development. As the authors say, “A better understanding of the
./technical/plos/pmed.0020023.txt:27:        paper the authors analyze the epidemic in sub-Saharan Africa (where three-fourths of deaths
./technical/plos/pmed.0020023.txt:30:        this region each year within the next two decades. The authors predicted that concentrating
./technical/plos/pmed.0020023.txt:39:        only one part of the equation. The authors comment that the mobilization of communities
./technical/plos/pmed.0020023.txt:42:        infected. As the authors say, only by doing so “will we at last move from slogans to
./technical/plos/pmed.0020024.txt:21:        What the authors found was that over the years 1994–2002, the week of the onset of the
./technical/plos/pmed.0020033.txt:91:        authors applied an array of cross-validation strategies that convincingly suggested that
./technical/plos/pmed.0020035.txt:44:        remit of the plan's authors was not to prescribe specific research but “to stimulate both
./technical/plos/pmed.0020036.txt:77:        The authors of the “The Global HIV/AIDS Vaccine Enterprise: Scientific Strategic Plan”
./technical/plos/pmed.0020039.txt:98:        The authors have demonstrated through mathematical modeling that the integration of
./technical/plos/pmed.0020050.txt:370:        Legitimate authorities in each nation must come to their own consensus on the priorities
./technical/plos/pmed.0020050.txt:373:        access (compensating for geographical isolation), but if authorities in a given nation
./technical/plos/pmed.0020055.txt:18:        datasets and complex analyses from these studies have presented challenges: for authors in
./technical/plos/pmed.0020055.txt:58:        case by case basis, which may not be reproducible, even by the authors. Some researchers
./technical/plos/pmed.0020055.txt:60:        entire analysis quickly and, hence, assess the robustness of the results. Some authors have
./technical/plos/pmed.0020055.txt:62:        (e.g., Nucleic Acids Res 32: e50). At the very least authors should have a protocol with a
./technical/plos/pmed.0020055.txt:69:        PLoS Medicine is keen to work with authors towards making such reporting
./technical/plos/pmed.0020061.txt:145:        subject to an authorization procedure to show that they can be used safely or that there
./technical/plos/pmed.0020061.txt:199:        tobacco, the US EPA and FDA need more authority and resources to regulate and reduce
./technical/plos/pmed.0020065.txt:8:        cases or clusters of cases of particular diseases to health-care and other authorities. The
./technical/plos/pmed.0020065.txt:38:        seems to perform well. As the authors discuss, as any other surveillance method, theirs has
./technical/plos/pmed.0020075.txt:85:        KRAS alleles that have previously been shown by these same authors to
./technical/plos/pmed.0020088.txt:11:        We ask all authors and reviewers to declare any competing interests—financial, personal,
./technical/plos/pmed.0020088.txt:12:        and professional [2]—and authors' declarations are included with all published articles. We
./technical/plos/pmed.0020088.txt:13:        reject articles when we believe that authors' competing interests have compromised their
./technical/plos/pmed.0020088.txt:22:        and the reputation of authors and of 
./technical/plos/pmed.0020088.txt:24:        evidence that authors' competing interests have a strong influence on their conclusions.
./technical/plos/pmed.0020088.txt:28:        whether an author was affiliated with the tobacco industry [5]. A study of 159 randomized
./technical/plos/pmed.0020088.txt:29:        clinical trials found a significant association between authors' financial competing
./technical/plos/pmed.0020088.txt:42:        the authors having disclosed a financial competing interest [7]. Readers scored the
./technical/plos/pmed.0020088.txt:45:        Our policy of asking authors to disclose their competing interests is not, of course,
./technical/plos/pmed.0020088.txt:47:        four scientific journals and identified at least 13 articles for which authors did not
./technical/plos/pmed.0020088.txt:50:        of the authors of a 2003 
./technical/plos/pmed.0020088.txt:52:        industry documents describing financial ties between the industry and the authors [9].
./technical/plos/pmed.0020088.txt:53:        Although the authors met the 
./technical/plos/pmed.0020088.txt:56:        authors.
./technical/plos/pmed.0020088.txt:57:        Should we as journal editors be investigating authors' ties for ourselves? We do not
./technical/plos/pmed.0020088.txt:60:        the authors, a quick search of the tobacco documents that are freely available online
./technical/plos/pmed.0020088.txt:69:        Others are more complex. When editors discover that a published author failed to declare a
./technical/plos/pmed.0020088.txt:71:        author? Should they publish a correction or even retract the paper?
./technical/plos/pmed.0020091.txt:20:        Haubner and colleagues, the authors of a paper in this month's 
./technical/plos/pmed.0020091.txt:35:        tumors including melanoma, the authors found a good deal of difference between patients in
./technical/plos/pmed.0020094.txt:35:        suppressing T cell sensitivity to stimulation. Finally, the authors found that the degree
./technical/plos/pmed.0020098.txt:87:        significant dropout rate that the authors assumed was random, a short follow-up period, and
./technical/plos/pmed.0020114.txt:32:        SP, said the authors. Other studies have already shown the potential of co-artemether
./technical/plos/pmed.0020114.txt:34:        authors. However, this study is the first to demonstrate the treatment's potential to
./technical/plos/pmed.0020114.txt:39:        malaria in Africa? The authors are hesitant and suggest there might be compliance issues
./technical/plos/pmed.0020114.txt:42:        The authors suggest that co-artemether as a first-line treatment is not likely to reduce
./technical/plos/pmed.0020117.txt:39:        However, the authors emphasize that differences in the types and patterns of
./technical/plos/pmed.0020120.txt:9:        stenosis) needs to be ruled out. Unfortunately, the authors perpetuate the extremely common
./technical/plos/pmed.0020144.txt:16:        meningococcal meningitis, the authors found that the timing of epidemics is highly
./technical/plos/pmed.0020146.txt:26:        overestimate. This estimate, the authors suggest, “is another example where the research
./technical/plos/pmed.0020146.txt:30:        reality is somewhat lower, and the authors suggest that “if we wish to provide the general
./technical/plos/pmed.0020146.txt:34:        The authors were surprised to find no difference in prevalence between males and
./technical/plos/pmed.0020146.txt:44:        authors conclude that “many people with schizophrenia have persisting symptoms, despite the
./technical/plos/pmed.0020146.txt:46:        can at most reduce 25% of disease burden, thus the authors conclude that “this is a
./technical/plos/pmed.0020148.txt:33:        pattern, but with some delay. The authors also found an inverse relationship between
./technical/plos/pmed.0020148.txt:41:        nations, the authors say. Demographic and technological changes are increasingly modifying
./technical/plos/pmed.0020148.txt:46:        diseases of the poor, the authors warn. (See also the Perspective by Thomas Novotny [DOI:
./technical/plos/pmed.0020149.txt:34:        As the authors declare, the study was funded by a maker of one of the statins, but the
./technical/plos/pmed.0020149.txt:37:        statins when indicated, the authors say. A particular focus should be patients who are at
./technical/plos/pmed.0020150.txt:36:        The authors admit that this observation could be due to any factor that affects malaria
./technical/plos/pmed.0020150.txt:42:        In discussing their findings the authors point out that their study focused on mild
./technical/plos/pmed.0020150.txt:48:        The authors conclude that the relevance of their current observations on mild clinical
./technical/plos/pmed.0020155.txt:74:        authorities in the many resource-constrained countries who will soon have to make very
./technical/plos/pmed.0020158.txt:67:        confidential to each journal. But if an author would like a manuscript that is not thought
./technical/plos/pmed.0020158.txt:74:        ambitious plan, but one that we believe will provide authors with more choices and in the
./technical/plos/pmed.0020180.txt:67:        IUFDs, exhibited signs of TTTS. The authors concluded that despite intensive fetal
./technical/plos/pmed.0020180.txt:70:        after 32 weeks' gestation. As a result, the authors suggested that after 32 weeks'
./technical/plos/pmed.0020180.txt:81:        monochorionic twins? The authors suggest that 32 weeks' gestation may be reasonable. At
./technical/plos/pmed.0020181.txt:40:        study, the authors appropriately excluded people with diabetes, and adjustment for
./technical/plos/pmed.0020181.txt:45:        to lose weight as a means to improve health. The authors' keen recognition of this problem
./technical/plos/pmed.0020181.txt:46:        provides a significant strength to the present study. The authors appropriately excluded
./technical/plos/pmed.0020181.txt:58:        weight, the authors identified individuals with intent to lose weight. Unintended weight
./technical/plos/pmed.0020187.txt:29:        used, the authors were able to plausibly conclude that the difference between the two
./technical/plos/pmed.0020187.txt:47:        The authors of the VIGOR study said, “We could not include a placebo group” [12]. Was
./technical/plos/pmed.0020191.txt:13:        meta-question: who is to decide who is to decide? I apologize to the authors if my brief
./technical/plos/pmed.0020192.txt:8:        the Dead to Make Medical Diagnoses” [1]. As a co-author of the 
./technical/plos/pmed.0020194.txt:47:        activity, say the authors. But they concede it is still unclear whether the enhancement of
./technical/plos/pmed.0020194.txt:59:        In discussing their findings, the authors suggest that their study supports previous
./technical/plos/pmed.0020195.txt:27:        The authors conclude that “despite intensive fetal surveillance, structurally normal
./technical/plos/pmed.0020195.txt:30:        the deaths occurred predominantly after 32 weeks' gestation, the authors suggest that the
./technical/plos/pmed.0020197.txt:69:        This case report has been reported to the regulatory authorities and to the manufacturer
./technical/plos/pmed.0020198.txt:44:        The authors conclude that these findings support the hypothesis that cardiovascular risk
./technical/plos/pmed.0020198.txt:53:        prominent goal of public policy, and the authors conclude that policymakers must pursue
./technical/plos/pmed.0020200.txt:22:        authors gathered data from the 2,957 overweight participants who remained after they had
./technical/plos/pmed.0020200.txt:26:        authors then analyzed mortality in relation to intention to lose weight and actual weight
./technical/plos/pmed.0020200.txt:43:        excess mortality. The authors suggest that this could be due to the unavoidable loss of
./technical/plos/pmed.0020200.txt:45:        may outweigh the beneficial effects of losing fat mass in healthy individuals. The authors
./technical/plos/pmed.0020201.txt:31:        authors then cultured these polyclonal precursors with appropriate tissue-specific
./technical/plos/pmed.0020201.txt:33:        the authors provide for these cells being differentiated includes analysis of gene
./technical/plos/pmed.0020201.txt:35:        example, the authors were able to show the presence of fat granules in adipocytes, calcium
./technical/plos/pmed.0020201.txt:40:        potential for residual undifferentiated cells to turn into tumors, but the authors tested
./technical/plos/pmed.0020201.txt:46:        the authors comment, “the high purity, unlimited availability, and multipotentiality of
./technical/plos/pmed.0020203.txt:43:        ethical conduct of the study and approval by the respective regulatory authority, but also
./technical/plos/pmed.0020203.txt:61:        with authors on a case-by-case basis. In addition, we currently cross-reference studies
./technical/plos/pmed.0020208.txt:60:        statutory authorities [12,13].
./technical/plos/pmed.0020209.txt:118:            Drug User Fee Act, and Graham argued that there needs to be independent authority for
./technical/plos/pmed.0020231.txt:36:        In the study by Mair et al., the authors examined life span in fruit flies (
./technical/plos/pmed.0020231.txt:39:        sugar only, and (4) restricted in yeast and sugar. The authors observed that in the
./technical/plos/pmed.0020231.txt:43:        yeast and sugar group (Figure 1). Importantly, the authors claim that total calorie
./technical/plos/pmed.0020231.txt:47:        It is of concern that the authors did not directly measure the flies' total food intake
./technical/plos/pmed.0020235.txt:20:        population matched on early life experiences, the authors say.
./technical/plos/pmed.0020235.txt:48:        authors say.
./technical/plos/pmed.0020236.txt:46:        malaria control measures, such as bed nets, said the authors.
./technical/plos/pmed.0020236.txt:53:        be long or short acting remains unclear, said the authors.
./technical/plos/pmed.0020236.txt:54:        Altogether, artemisinin combinations offer great hope for Africa, the authors say,
./technical/plos/pmed.0020237.txt:41:        exploration, the authors say, concluding that viral replication efficiency was determined
./technical/plos/pmed.0020237.txt:50:        The authors conclude that the future of long-term viral clearance will require
./technical/plos/pmed.0020238.txt:26:        fundamentally changed in the wake of several major new trials. The authors searched the
./technical/plos/pmed.0020238.txt:40:        Altogether, the authors conclude that the evidence base supports the first-line use of a
./technical/plos/pmed.0020238.txt:47:        hazardous, and the authors and other researchers have concluded that further high-quality
./technical/plos/pmed.0020238.txt:48:        trials of this therapy are needed. The authors found little evidence regarding possible
./technical/plos/pmed.0020239.txt:21:        The authors warn that if such biases are not corrected, health authorities risk making
./technical/plos/pmed.0020239.txt:29:        authors, who suggest instead that it would more sensible to specify the probability of
./technical/plos/pmed.0020239.txt:34:        The authors also note another issue that has received surprisingly little attention in
./technical/plos/pmed.0020239.txt:40:        public health concerns, say the authors. They tested their theory by using analytical
./technical/plos/pmed.0020239.txt:58:        authors note that while some practitioners are using their approach, most applied
./technical/plos/pmed.0020239.txt:60:        incubation and infectious periods; the authors hope their work will point to the next steps
./technical/plos/pmed.0020242.txt:68:        to pediatric patients. “Despite these reservations,” he says, “the authors of this study
./technical/plos/pmed.0020246.txt:121:          Ministry of Health, state and local government authorities, and facility directors. There
./technical/plos/pmed.0020246.txt:414:        Cultural Rights and the authoritative interpretations of the ESCR Committee. This study
./technical/plos/pmed.0020247.txt:89:        Punishment theories authorize communities to isolate or purge the “impure”—people whose
./technical/plos/pmed.0020257.txt:51:        behavior and/or an overreporting of “correct” practices or attitudes. The authors note that
./technical/plos/pmed.0020258.txt:41:        authors have made available the programming script of their analysis so anyone can repeat
./technical/plos/pmed.0020268.txt:51:        research tool to stratify patients' parasite loads, say the authors. They conclude that
./technical/plos/pmed.0020272.txt:6:        Scientific truth is a moving target. In the process of peer review, authors, reviewers,
./technical/plos/pmed.0020272.txt:69:        comfortable with uncertainty. We encourage authors to discuss biases, study limitations,
./technical/plos/pmed.0020273.txt:32:        compared with 42% of genes in UC. However, the authors caution that this finding was highly
./technical/plos/pmed.0020274.txt:38:        to follow these trends, said the authors.
./technical/plos/pmed.0020274.txt:39:        However, the authors warned that the high percentage of HCoV-NL63-positive samples could
./technical/plos/pmed.0020274.txt:44:        authorities should add HCoV-NL63 to the list of pathogens that can cause numerous LRTIs in
./technical/plos/pmed.0020275.txt:36:        years and above. The authors estimate that around 163,000 new cases of dementia occur in
```
This example printed out the line and line number where "author" was matched in every .txt file in /technical/plos. This is useful if we want to find the line number where an author is mentioned.



