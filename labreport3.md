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






