/*
 * To change this template, choose Tools | Templates
 * and open the template in the editor.
 */
package jshell;

import java.util.ArrayList;
import org.junit.After;
import org.junit.AfterClass;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;
import static org.junit.Assert.*;

/**
 *
 * @author Daniel Bild-Enkin
 */
public class DirTrieTest {

    public DirTrieTest() {
    }

    @BeforeClass
    public static void setUpClass() throws Exception {
    }

    @AfterClass
    public static void tearDownClass() throws Exception {
    }

    @Before
    public void setUp() {
    }

    @After
    public void tearDown() {
    }

    /**
     * returns arbitrary-ish tree for testing purposes with the nodes explicitely visible
     * @return arbitrary-ish tree for testing purposes with the nodes explicitely visible
     */
    private static Node[] creatTestTree(DirTrie dirtrie) {

        Node[] return_value = new Node[12];

        /*this is the tree created with node names
         *                               root
         *                                1
         *                        /                \
         *                        n2              node12
         *                  /     |    \
         *               node3  node4  node5
         *                /     /   \    \
         *             node6 node7 node8 node9
         *                               /   \
         *                            node10 node11
         */

        // Set up tree with nodes visible
        // testing various name lengths
        return_value[0] = new Node(dirtrie.getRoot(), "1");
        return_value[1] = new Node(return_value[0], "n2");
        return_value[2] = new Node(return_value[1], "node3");
        return_value[3] = new Node(return_value[1], "node4");
        return_value[4] = new Node(return_value[1], "node5");
        return_value[5] = new Node(return_value[2], "node6");
        return_value[6] = new Node(return_value[3], "node7");
        return_value[7] = new Node(return_value[3], "node8");
        return_value[8] = new Node(return_value[4], "node9");
        return_value[9] = new Node(return_value[8], "node10");
        return_value[10] = new Node(return_value[8], "node11");
        return_value[11] = new Node(return_value[0], "node12");

        for (Node node : return_value) {
            node.attachNode();
        }

        return return_value;

    }

    /**
     * Test of checkExist method, of class DirTrie for absolute paths.
     */
    @Test
    public void testCheckExistAbsolute() {
        System.out.println("CheckExistAbsolute");
        DirTrie dirtrie = new DirTrie();
        Node[] tree = creatTestTree(dirtrie);

        assertEquals(dirtrie.getRoot(), dirtrie.checkExist("/"));
        assertEquals(tree[0], dirtrie.checkExist("/1"));
        assertEquals(tree[1], dirtrie.checkExist("/1/n2"));
        assertEquals(tree[2], dirtrie.checkExist("/1/n2/node3"));
        assertEquals(tree[3], dirtrie.checkExist("/1/n2/node4"));
        assertEquals(tree[4], dirtrie.checkExist("/1/n2/node5"));
        assertEquals(tree[5], dirtrie.checkExist("/1/n2/node3/node6"));
        assertEquals(tree[6], dirtrie.checkExist("/1/n2/node4/node7"));
        assertEquals(tree[7], dirtrie.checkExist("/1/n2/node4/node8"));
        assertEquals(tree[8], dirtrie.checkExist("/1/n2/node5/node9"));
        assertEquals(tree[9], dirtrie.checkExist("/1/n2/node5/node9/node10"));
        assertEquals(tree[10], dirtrie.checkExist("/1/n2/node5/node9/node11"));
        assertEquals(tree[11], dirtrie.checkExist("/1/node12"));
        //test checkExist for absolute paths with ..
        assertEquals(tree[0], dirtrie.checkExist("/1/node12/.."));
        //Test checkExist for incorrect absolute paths
        assertEquals(null, dirtrie.checkExist("/1/node13"));
        assertEquals(null, dirtrie.checkExist("/1/n3/node5/node9/node11"));
        //Test checkExist for incorrect absolute paths with ..
        assertEquals(null, dirtrie.checkExist("/1/node13/.."));
    }

    /**
     * Test of checkExist method, of class DirTrie for relative paths.
     */
    @Test
    public void testCheckExistRelative() {
        DirTrie dirtrie = new DirTrie();
        Node[] tree = creatTestTree(dirtrie);
        //Test checkExist for relative paths
        String[] str = new String[1];
        str[0] = "/1/n2/node5";

        dirtrie.changeDir(str);
        assertEquals(tree[4], dirtrie.checkExist(""));
        assertEquals(tree[8], dirtrie.checkExist("node9"));
        assertEquals(tree[9], dirtrie.checkExist("node9/node10"));
        assertEquals(tree[10], dirtrie.checkExist("node9/node11"));
        //Test checkExist for relative paths from root
        String[] rootStr = new String[1];
        rootStr[0] = "/";
        dirtrie.changeDir(rootStr);
        assertEquals(tree[0], dirtrie.checkExist("1"));
        //test checkExist for incorrect relative paths
        dirtrie.changeDir(str);
        assertEquals(null, dirtrie.checkExist("node10"));
        assertEquals(null, dirtrie.checkExist("node8/node11"));
        //test checkExist for relative paths with ..
        assertEquals(tree[1], dirtrie.checkExist(".."));
        assertEquals(tree[2], dirtrie.checkExist("../node3"));
        //test checkExist for relative paths with .. past root
        assertEquals(dirtrie.getRoot(), dirtrie.checkExist("../../../.."));
        //test checkExist for incorect relative paths with ..
        assertEquals(null, dirtrie.checkExist("../../node13"));
        assertEquals(null, dirtrie.checkExist("../../../1/n1"));
        assertEquals(null, dirtrie.checkExist("../../../2/n2"));
        //test checkExist for relative paths with .. after other path
        assertEquals(tree[0], dirtrie.checkExist("../../n2/.."));
        //test checkExist for incorrect relative paths with .. after other path
        assertEquals(null, dirtrie.checkExist("../../2/n2/.."));
        // test checkExist for paths with / at the end
        assertEquals(tree[0], dirtrie.checkExist("/1/"));
    }

    /**
     * tests whether node gone to by changdir(cur_dir_path) is equal to correct_node
     * @param dirtrie current instance of class DirTrie
     * @param correct_node correct value of to be returned by changdir
     * @param cur_dir_path path of node
     */
    private static void changeDirAbsoluteTestHelp(DirTrie dirtrie, Node correct_node, String cur_dir_path) {
        String[] str = new String[1];
        str[0] = cur_dir_path;


        dirtrie.changeDir(str);
        assertEquals(correct_node, dirtrie.getCurrent());
    }

    /**
     * Test of changeDir method, of class DirTrie for absolute paths.
     */
    @Test
    public void testChangeDirAbsolute() {
        System.out.println("changeDirAbsolute");
        DirTrie dirtrie = new DirTrie();
        Node[] tree = creatTestTree(dirtrie);
        //test that cd / goes to home
        changeDirAbsoluteTestHelp(dirtrie, dirtrie.getRoot(), "/");
        changeDirAbsoluteTestHelp(dirtrie, tree[0], "/1");
        // show that first cd / actualy goes home and not just chance
        changeDirAbsoluteTestHelp(dirtrie, dirtrie.getRoot(), "/");
        changeDirAbsoluteTestHelp(dirtrie, tree[1], "/1/n2");
        changeDirAbsoluteTestHelp(dirtrie, tree[2], "/1/n2/node3");
        changeDirAbsoluteTestHelp(dirtrie, tree[3], "/1/n2/node4");
        changeDirAbsoluteTestHelp(dirtrie, tree[4], "/1/n2/node5");
        changeDirAbsoluteTestHelp(dirtrie, tree[5], "/1/n2/node3/node6");
        changeDirAbsoluteTestHelp(dirtrie, tree[6], "/1/n2/node4/node7");
        changeDirAbsoluteTestHelp(dirtrie, tree[7], "/1/n2/node4/node8");
        changeDirAbsoluteTestHelp(dirtrie, tree[8], "/1/n2/node5/node9");
        changeDirAbsoluteTestHelp(dirtrie, tree[9], "/1/n2/node5/node9/node10");
        changeDirAbsoluteTestHelp(dirtrie, tree[10], "/1/n2/node5/node9/node11");
        changeDirAbsoluteTestHelp(dirtrie, tree[11], "/1/node12");
        // test cd + absolute path with ..
        changeDirAbsoluteTestHelp(dirtrie, tree[1], "/1/n2/node3/..");
        //test cd + incorrect absolute path

        String[] str = new String[1];
        str[0] = "/";
        dirtrie.changeDir(str);
        changeDirAbsoluteTestHelp(dirtrie, dirtrie.getRoot(), "/1/n3");
        changeDirAbsoluteTestHelp(dirtrie, dirtrie.getRoot(), "/2/n2");
        // test cd + incorrect absolute path with ..
        changeDirAbsoluteTestHelp(dirtrie, dirtrie.getRoot(), "/2/..");
    }

    /**
     * 
     * tests whether node gone to by changdir(cur_dir_path) is equal to correct_node
     * @param dirtrie current instance of class DirTrie
     * @param correct_node correct_node correct value of to be returned by changdir
     * @param cur_dir_path1 path of node from which other path is relative
     * @param cur_dir_path2 relative path of node
     */
    private static void changeDirRelativeTestHelp(DirTrie dirtrie, Node correct_node,
            String cur_dir_path1, String cur_dir_path2) {

        String[] str1 = new String[1];
        String[] str2 = new String[1];
        str1[0] = cur_dir_path1;
        str2[0] = cur_dir_path2;
        dirtrie.changeDir(str1);
        dirtrie.changeDir(str2);
        assertEquals(correct_node, dirtrie.getCurrent());

    }

    /**
     * Test of changeDir method of class DirTrie for relative paths.
     */
    @Test
    public void testChangeDirRelative() {
        System.out.println("changeDirRelative");
        DirTrie dirtrie = new DirTrie();
        Node[] tree = creatTestTree(dirtrie);
        changeDirRelativeTestHelp(dirtrie, tree[8], "/1/n2/node5", "node9");
        changeDirRelativeTestHelp(dirtrie, tree[9], "/1/n2/node5", "node9/node10");
        changeDirRelativeTestHelp(dirtrie, tree[10], "/1/n2/node5", "node9/node11");
        //test cd + relative path from root
        changeDirRelativeTestHelp(dirtrie, tree[0], "/", "1");
        //test cd + relative path with ..
        changeDirRelativeTestHelp(dirtrie, tree[1], "/1/n2/node5", "..");
        changeDirRelativeTestHelp(dirtrie, tree[0], "/1/n2/node5", "../..");
        changeDirRelativeTestHelp(dirtrie, dirtrie.getRoot(),
                "/1/n2/node5", "../../..");
        changeDirRelativeTestHelp(dirtrie, tree[2], "/1/n2/node5", "../node3");
        changeDirRelativeTestHelp(dirtrie, tree[11], "/1/n2/node5", "../../node12");
        //test cd + .. past root 
        changeDirRelativeTestHelp(dirtrie, dirtrie.getRoot(),
                "/1/n2/node5", "../../../..");
        //test cd + incorect relative path with ..
        changeDirRelativeTestHelp(dirtrie, tree[4], "/1/n2/node5", "../../../2");
        changeDirRelativeTestHelp(dirtrie, tree[4], "/1/n2/node5", "../../../1/n3");
        changeDirRelativeTestHelp(dirtrie, tree[4], "/1/n2/node5", "../../../2/n2");
    }

    /**
     * test whether makeDir creates new node with a name dirname 
     * and with a parent whose path is parentpath
     * @param dirtrie current instance of class DirTrie
     * @param parentpath path to parent of new node
     * @param dirname name of new node
     */
    private static void makeDirTestAbsoluteCorrectHelp(DirTrie dirtrie,
            String parentpath, String dirname) {
        String[] str = new String[1];
        int oldlength;
        int newlength;
        str[0] = parentpath + "/" + dirname;

        oldlength = dirtrie.checkExist(parentpath).getChildren().size();
        dirtrie.makeDir(str);
        newlength = dirtrie.checkExist(parentpath).getChildren().size();
        assertEquals(oldlength + 1, newlength);
        assertEquals(dirname, dirtrie.checkExist(str[0]).getName());
    }

    /**
     * test whether makeDir creates new node with name dirname
     * and  parent whose path relative to curdir is parentpath
     * @param curdir current node from which parentpath is relative
     * @param parentpath path to parent of new node
     * @param dirname name of new node
     */
    private static void makeDirTestRelativeCorrectHelp(DirTrie dirtrie,
            String curdir, String parentpath, String dirname) {

        String[] str = new String[1];
        str[0] = curdir;
        dirtrie.changeDir(str);
        String[] str1 = new String[1];
        int oldlength;
        int newlength;
        if (parentpath.isEmpty()) {
            str1[0] = dirname;
        } else {
            str1[0] = parentpath + "/" + dirname;
        }

        oldlength = dirtrie.checkExist(parentpath).getChildren().size();
        dirtrie.makeDir(str1);
        newlength = dirtrie.checkExist(parentpath).getChildren().size();
        assertEquals(oldlength + 1, newlength);
        assertEquals(dirname, dirtrie.checkExist(str1[0]).getName());
    }

    /**
     * test whether makeDir creates nothing 
     * and that the path correct_parentpath/wrong_dir/dirname does not exist
     * when wrong_dir is not in the tree
     * @param correct_parentpath path up to incorrect part
     * @param wrong_dir path including and after incorrect part
     * @param dirname name of new (non-existant) node
     */
    private static void makeDirTestAbsoluteIncorrectHelp(DirTrie dirtrie,
            String correct_parentpath, String wrong_dir, String dirname) {
        int oldlength;
        int newlength;
        String[] str = new String[1];

        str[0] = correct_parentpath + "/" + wrong_dir + "/" + dirname;

        oldlength = dirtrie.checkExist(correct_parentpath).getChildren().size();
        dirtrie.makeDir(str);
        newlength = dirtrie.checkExist(correct_parentpath).getChildren().size();
        // 1  and n2 have no extra children and /1/n1/node3 does not exist
        assertEquals(oldlength, newlength);
        assertEquals(null, dirtrie.checkExist(str[0]));
    }

    /**
     * Test that makeDir creates nothing and that the path's relative to curdir, 
     * correct_parentpath/wrong_dir/dirname does not exist when wrong_dir 
     * is not in the tree
     * @param curdir current node from which correct_parentpath is relative
     * @param correct_parentpath path up to incorrect part
     * @param wrong_dir path including and after incorrect part
     * @param dirname name of new (non-existant) node
     */
    private static void makeDirTestRelativeIncorrectHelp(DirTrie dirtrie,
            String curdir, String correct_parentpath, String wrong_dir, String dirname) {

        String[] str = new String[1];
        str[0] = curdir;
        dirtrie.changeDir(str);
        int oldlength;
        int newlength;
        String[] str1 = new String[1];

        if (correct_parentpath.isEmpty()) {
            str1[0] = wrong_dir + "/" + dirname;
        } else {
            str1[0] = correct_parentpath + "/" + wrong_dir + "/" + dirname;
        }

        oldlength = dirtrie.checkExist(correct_parentpath).getChildren().size();
        dirtrie.makeDir(str1);
        newlength = dirtrie.checkExist(correct_parentpath).getChildren().size();
        // 1  and n2 have no extra children and /1/n1/node3 does not exist
        assertEquals(oldlength, newlength);
        assertEquals(null, dirtrie.checkExist(str1[0]));
    }

    /**
     * Test of makeDir method, of class DirTrie.
     */
    @Test
    public void testMakeDir() {
        System.out.println("makeDir");
        DirTrie dirtrie = new DirTrie();

        //makeDir with absolute path
        makeDirTestAbsoluteCorrectHelp(dirtrie, "", "1");
        makeDirTestAbsoluteCorrectHelp(dirtrie, "/1", "n2");
        //makedir with incorect parent absolute path
        makeDirTestAbsoluteIncorrectHelp(dirtrie, "", "2", "n2");
        // makeDir with relative path 
        makeDirTestRelativeCorrectHelp(dirtrie, "/1", "", "node12");
        makeDirTestRelativeCorrectHelp(dirtrie, "/1", "n2", "node4");
        // makeDir with incorect relative path
        makeDirTestRelativeIncorrectHelp(dirtrie, "/1", "", "n1", "node3");

        int oldlength;
        int newlength;
        int oldlength1;
        int newlength1;
        String[] str = new String[1];
        String[] str1 = new String[1];

        // makeDir with duplicate path name
        str[0] = "1";
        str1[0] = "/";
        dirtrie.changeDir(str1);
        oldlength = dirtrie.getCurrent().getChildren().size();
        dirtrie.makeDir(str);
        newlength = dirtrie.getCurrent().getChildren().size();
        assertEquals(oldlength, newlength);

        // makeDir with multiple paths entered
        str[0]="/1/n2";
        dirtrie.changeDir(str);
        str1 = new String[3];
        str1[0] = "node4/node6"; // normal valid relative case
        str1[1] = "/1/n2/node4/node7"; // normal valid absolute case
        str1[2] = "../node5/node6"; // incorrect relative case

        oldlength = dirtrie.checkExist("/1/n2/node4").getChildren().size();
        int oldlength2 = dirtrie.checkExist("/1").getChildren().size();
        dirtrie.makeDir(str1);
        newlength = dirtrie.checkExist("/1/n2/node4").getChildren().size();
        int newlength2 = dirtrie.checkExist("/1").getChildren().size();
        assertEquals(oldlength + 2, newlength);

        assertEquals(oldlength2, newlength2);
        assertEquals(null, dirtrie.checkExist("/1/node5/node6"));
    }

    /**
     * Test of listFile method, of class DirTrie.
     */
    @Test
    public void testListFile() {
        System.out.println("listFile");
        DirTrie dirtrie = new DirTrie();
        Node[] tree = creatTestTree(dirtrie);

        //no path
        String[] str = new String[1];
        str[0]="/1/n2";
        dirtrie.changeDir(str);
        
        str = new String[0];
        String test_str = dirtrie.listFile(str);
        String correct_str = "node3\nnode4\nnode5\n";
        assertEquals(test_str, correct_str);

        //absolute path
        str = new String[1];
        str[0] = "/1/n2";
        test_str = dirtrie.listFile(str);
        correct_str = "n2: node3 node4 node5 \n";
        assertEquals(test_str, correct_str);

        //relative path
        str[0] = "node3";
        test_str = dirtrie.listFile(str);
        correct_str = "node3: node6 \n";
        assertEquals(test_str, correct_str);

        //incorect path 
        str[0] = "node6";
        test_str = dirtrie.listFile(str);
        correct_str = "ls: node6: Path does not exist\n";
        assertEquals(test_str, correct_str);

        //too many path 
        str = new String[2];
        str[0] = "node6";
        str[1] = "node3";
        test_str = dirtrie.listFile(str);
        correct_str = "ls: node6: Path does not exist\nnode3: node6 \n";
        System.out.println(test_str);
        System.out.println(correct_str);
        assertEquals(test_str, correct_str);



    }
}
