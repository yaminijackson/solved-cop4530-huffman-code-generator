Download Link: https://assignmentchef.com/product/solved-cop4530-huffman-code-generator
<br>
For Programming Project 4, you will be generating Huffman codes to compress a given string. A Huffman code uses a set of prefix code to compress the string with no loss of data (lossless).

David Huffman developed this algorithm in the paper “A Method for the Construction of Minimum-Redundancy Codes” (<a href="http://compression.ru/download/articles/huff/huffman_1952_minimum-redundancy-codes.pdf">http://compression.ru/download/articles/huff/ </a><a href="http://compression.ru/download/articles/huff/huffman_1952_minimum-redundancy-codes.pdf">huffman_1952_minimum-redundancy-codes.pdf</a>)

A program can generate Huffman codes from a string using the following steps:

<ul>

 <li>Generate a list of the frequency in which characters appear in the string using a map</li>

 <li>Inserting the characters and their frequencies into a priority queue (sorted first by the lowest frequency and then lexicographically)</li>

 <li>Until there is one element left in the priority queue</li>

 <li>Remove two characters/frequencies pairs from the priority queue</li>

 <li>Turn them into leaf nodes on a binary tree</li>

 <li>Create an intermediate node to be their parent using the sum of the frequencies for those children</li>

 <li>Put that intermediate node back in the priority queue</li>

 <li>The last pair in the priority queue is the root node of the tree</li>

 <li>Using this new tree, encode the characters in the string using a map with their prefix code by traversing the tree to find where the character’s leaf is. When traversal goes left, add a 0 to the code, when it goes right, add a 1 to the code</li>

 <li>With this encoding, replace the characters in the string with their new variable-length prefix codes</li>

</ul>




In addition to the compress string, you will need to be able to serialize the tree. Without the serialized version of the Huffman tree, you will not be able to decompress the Huffman codes.

Tree serialization will organize the characters associated with the nodes using post order.

During the post order when you visit a node,

<ul>

 <li>if it the node is a leaf (external node) then you add a L plus the character to the serialize tree string</li>

 <li>if it is a branch (internal node) then you add a B to the serialize tree string</li>

</ul>

For decompression, two input arguments will be needed. The Huffman Code that was generated by your compress method and the serialized tree string from your serializeTree method. Your Huffman tree will have to be built by deserializing the tree string by using the leaves and branches indicators. After you have your tree back, you can decompress the Huffman Code by tracing the tree to figure out what variable length codes represent actual characters from the original string.

So, for example, if we are compressing the string “if a machine is expected to be infallible it cannot also be intelligent”:

Our compress algorithm would generate the following codes for the characters:

<table width="624">

 <tbody>

  <tr>

   <td width="208"><strong>Character</strong></td>

   <td width="208"><strong>Frequency</strong></td>

   <td width="208"><strong>Prefix Code</strong></td>

  </tr>

  <tr>

   <td width="208"><strong>(space) </strong></td>

   <td width="208">12</td>

   <td width="208">00</td>

  </tr>

  <tr>

   <td width="208"><strong>a       </strong></td>

   <td width="208">5</td>

   <td width="208">1011</td>

  </tr>

  <tr>

   <td width="208"><strong>b       </strong></td>

   <td width="208">3</td>

   <td width="208">10101</td>

  </tr>

  <tr>

   <td width="208"><strong>c       </strong></td>

   <td width="208">3</td>

   <td width="208">11000</td>

  </tr>

  <tr>

   <td width="208"><strong>d       </strong></td>

   <td width="208">1</td>

   <td width="208">010000</td>

  </tr>

  <tr>

   <td width="208"><strong>e       </strong></td>

   <td width="208">9</td>

   <td width="208">100</td>

  </tr>

  <tr>

   <td width="208"><strong>f       </strong></td>

   <td width="208">2</td>

   <td width="208">01011</td>

  </tr>

  <tr>

   <td width="208"><strong>g       </strong></td>

   <td width="208">1</td>

   <td width="208">010001</td>

  </tr>

  <tr>

   <td width="208"><strong>h       </strong></td>

   <td width="208">1</td>

   <td width="208">010010</td>

  </tr>

  <tr>

   <td width="208"><strong>i       </strong></td>

   <td width="208">8</td>

   <td width="208">011</td>

  </tr>

  <tr>

   <td width="208"><strong>l       </strong></td>

   <td width="208">6</td>

   <td width="208">1101</td>

  </tr>

  <tr>

   <td width="208"><strong>m       </strong></td>

   <td width="208">1</td>

   <td width="208">010011</td>

  </tr>

  <tr>

   <td width="208"><strong>n       </strong></td>

   <td width="208">6</td>

   <td width="208">1110</td>

  </tr>

  <tr>

   <td width="208"><strong>o       </strong></td>

   <td width="208">3</td>

   <td width="208">11001</td>

  </tr>

  <tr>

   <td width="208"><strong>p       </strong></td>

   <td width="208">1</td>

   <td width="208">010100</td>

  </tr>

  <tr>

   <td width="208"><strong>s       </strong></td>

   <td width="208">2</td>

   <td width="208">10100</td>

  </tr>

  <tr>

   <td width="208"><strong>t       </strong></td>

   <td width="208">6</td>

   <td width="208">1111</td>

  </tr>

  <tr>

   <td width="208"><strong>x       </strong></td>

   <td width="208">1</td>

   <td width="208">010101</td>

  </tr>

 </tbody>

</table>

Our code would be:

011010110010110001001110111100001001001111101000001110100001000101010101001001

1000111110001000000111111001001010110000011111001011101111011101011101011101100

00011111100110001011111011101100111110010111101101001100100101011000001111101111 1001101110101101000110011101111

And our serialize tree would look like:

L LdLgBLhLmBBLpLxBLfBBLiBBLeLsLbBLaBBLcLoBLlBLnLtBBBB

You will need to create one class for this project: HuffmanTree for the compression, decompression, and serialization that uses a linked binary tree. You are given a Heap-based Priority Queue for the sorting. You are allowed to use the STL map, vector, and stack, but not the STL priority queue.

<h2>Abstract Class Methods</h2>

<strong>std::string compress(const std::string inputStr) </strong>

Compress the input string using the method explained above. Note: Typically we would be returning a number of bits to represent the code, but for this project we are returning a string

<strong>std::string serializeTree() const </strong>

Serialize the tree using the above method. We do not need the frequency values to rebuild the tree, just the characters on the leaves and where the branches are in the post order.

<strong>std::string decompress(const std::string inputCode, const std::string serializedTree)  </strong>

Given a string created with the compress method and a serialized version of the tree, return the decompressed original string

<h2>Other things in Huffman hpp/cpp</h2>

To simplify the process, I have given the full interface and implementation for a class called HuffmanNode. This class has all the basics for a tree node (leaf, branch, root, data members for linking, accessor) and also includes a comparator class for use with the heap. You should not need to alter any of the code for this node.

<h1>Examples</h1>

Below are some examples of how your code will run <strong>HuffmanTree t; </strong>

<strong>string test = “It is time to unmask the computing community as a Secret Society for the Creation and Preservation of Artificial </strong>

<strong>Complexity”; </strong>

<strong>/* </strong>

<strong>1000101011110000101001100110000010111011001110111101111100011001001011</strong>

<strong>0100100001111001110010011101101111010110010101010111110011000001110000 1011011110101100100010111110001100001111111111001011010011001011101001</strong>

<strong>1111101111001001110011110100111101111110000111001111111111010101110110 1001100111001001110110100110010011100101011000101100111100101001110000</strong>

<strong>0111010000000100111010100111001001000110010101100010110011110101110101</strong>

<strong>1110100010001000110001010110001111000001011001011101001101011001010101</strong>

<strong>010010111101000111000011111111 */ string code = t.compress(test); </strong>

<strong>/* LiLmLnBBLrLaBLtBBLPLdBLgLkBBLALIBLvLxBBBLhLlBLCLSBBBLsLpLfBBLoBBL LeLcLuLyBBBBBB */ </strong>

<strong>string tree = t.serializeTree(); </strong>

<strong>/* It is time to unmask the computing community as a Secret Society for the Creation and Preservation of Artificial Complexity */ string orig = t.decompress(code, tree); </strong>

<h1>Deliverables</h1>

Please submit complete projects as zipped folders. The zipped folder should contain:

<ul>

 <li>cpp (Your written HuffmanTree class)</li>

 <li>hpp (Your written HuffmanTree class)</li>

 <li>hpp (The given Heap Priority Queue using an array/vector class)</li>

 <li>cpp (The provided base class and helper class)</li>

 <li>hpp (The provided base class and helper class)</li>

 <li>cpp (Test file)</li>

 <li>hpp (Test file)</li>

 <li>hpp (Catch2 Header)</li>

</ul>

And any additional source and header files needed for your project.

<h1>Hints</h1>

For the encoding step where you translate characters using your Huffman Tree, this is essentially a preordering of the tree and can be done recursively.

Remember, when you are deserializing, you are going from post ordering back to the full tree. This is very similar to the postfix to infix conversion you did in PP2, but now building a tree instead of an expression.

For decoding the characters, you just follow the tree down the branches until you hit the leaf with the character, adding a zero for a left move and adding a 1 for a right move.

I suggest implementing a recursive method to destroy nodes for your destructor.

For the branching nodes, I suggest using the null character just to hold a spot since this should not be popping up in text you are compressing.

The test cases are based on using the standard library header &lt;map&gt;, not the unordered map.

Additional resources:  <a href="https://en.wikipedia.org/wiki/Huffman_coding">https://en.wikipedia.org/wiki/Huffman_coding</a> <a href="https://www.youtube.com/watch?v=0kNXhFIEd_w">https://www.youtube.com/watch?v=0kNXhFIEd_w</a><u> </u>


