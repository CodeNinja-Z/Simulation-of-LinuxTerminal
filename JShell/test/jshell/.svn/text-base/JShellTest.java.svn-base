package jshell;

import org.junit.After;
import org.junit.AfterClass;
import org.junit.Before;
import org.junit.BeforeClass;
import org.junit.Test;
import static org.junit.Assert.*;

public class JShellTest {

    public JShellTest() {
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

    private static Node[] create_test_tree(DirTrie dirtrie) {

        Node[] return_value = new Node[12];

        /* Create the following tree:
         *                               root
         *                                1
         *                       /                  \
         *                       n2                node12
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
     * Test of main method, of class JShell.
     */
    @Test
    public void testMain_no_command() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("main");
        String[] args = null;
        assertEquals(true, jshell.getJ());

    }

    /**
     * Test of execute method exit, of class JShell.
     */
    @Test
    public void testExecuteExit() {
        JShell jshell = new JShell();
        System.out.println("execute_exit");
        String cmd = "exit";
        jshell.execute(cmd);
        assertEquals(false, jshell.getJ());
    }

    /**
     * Test of execute method mkdir with single path entered.
     */
    @Test
    public void testExecuteMkdirSingle() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("excute_mkdir_single");
        //String cmd = "cd 1";
        //jshell.execute(cmd);
        String cmd = "mkdir 1/node12/node13";
        jshell.execute(cmd);
        assertEquals("node13", jshell.getDirTrie().checkExist("1/node12/node13")
                .getName());
    }

    /*
     * Test of execute method mkdir with multiple paths.
     */
    @Test
    public void testExecuteMkdirMulti() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("excute_mkdir_multi");
        String cmd = "mkdir 1/node12/node13 1/node12/node14";
        jshell.execute(cmd);
        assertEquals("node13", jshell.getDirTrie().checkExist("1/node12/node13")
                .getName());
        assertEquals("node14", jshell.getDirTrie().checkExist("1/node12/node14")
                .getName());
    }

    /**
     * Test of execute method mkdir, with multiple paths one of which is 
     * incorrect.
     */
    @Test
    public void testExecuteMkdirMultiWrong() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("excuteMkdirMulti");
        String cmd = "mkdir 1/node12/node13 1/n3/node3";
        jshell.execute(cmd);
        assertEquals("node13", jshell.getDirTrie().checkExist("1/node12/node13")
                .getName());
        assertEquals(null, jshell.getDirTrie().checkExist("1/n3/node3"));
    }

    /**
     * Test of execute method mkdir with relative paths.
     */
    @Test
    public void testExecuteMkdirRelativeSingle() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("excute_mkdir_relative_single");
        String[] newDirectory = new String[1];
        newDirectory[0] = "1/n2";
        jshell.getDirTrie().changeDir(newDirectory);
        String cmd = "mkdir node4/node13";
        jshell.execute(cmd);
        assertEquals("node13", jshell.getDirTrie().checkExist("node4/node13")
                .getName());
    }

    /*
     * Test of execute method mkdir with multiple relative paths entered.
     */
    @Test
    public void testExecuteMkdirRelativeMulti() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("excute_mkdir_relative_multi");
        String[] newDirectory = new String[1];
        newDirectory[0] = "/1/n2";
        jshell.getDirTrie().changeDir(newDirectory);
        String cmd = "mkdir node4/node13 node4/node14";
        jshell.execute(cmd);
        assertEquals("node13", jshell.getDirTrie().checkExist("node4/node13")
                .getName());
        assertEquals("node14", jshell.getDirTrie().checkExist("node4/node14")
                .getName());
    }

    /*
     * Test of execute cd command moving down into the tree.
     */
    @Test
    public void testExecuteCdGoDown() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("excute_cd_go_down");
        String cmd = "cd 1";
        jshell.execute(cmd);
        cmd = "cd n2";
        jshell.execute(cmd);
        cmd = "cd node5";
        jshell.execute(cmd);
        assertEquals("node5", jshell.getDirTrie().getCurrent().getName());
    }

    /**
     * Test of execute cd command moving up "levels" using "..", 
     */
    @Test
    public void testExecuteCdGoUpper() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("excute_cd_go_upper");
        String cmd = "cd 1";
        jshell.execute(cmd);
        cmd = "cd n2";
        jshell.execute(cmd);
        cmd = "cd node5";
        jshell.execute(cmd);
        assertEquals("node5", jshell.getDirTrie().getCurrent().getName());
        cmd = "cd ..";
        jshell.execute(cmd);
        cmd = "cd ..";
        jshell.execute(cmd);
        assertEquals("1", jshell.getDirTrie().getCurrent().getName());

    }

    /**
     * Test of execute method with non-trivial path.
     */
    @Test
    public void testExecuteCdGoUpNDown() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("excute_cd_go_upper");
        String cmd = "cd 1/n2/./node3/./node6/../../node4/"
                + "node7/../../.././node12";
        jshell.execute(cmd);
        assertEquals("node12", jshell.getDirTrie().getCurrent().getName());
    }

    /**
     * Test of execute method with non-trivial invalid path.
     */
    @Test
    public void testExecuteCdGoNowhere() {
        JShell jshell = new JShell();
        create_test_tree(jshell.getDirTrie());
        System.out.println("excute_cd_go_nowhere");
        String cmd = "cd 1/n2/./node3/./node6/../../node4/"
                + "node7/../../.././node11";
        jshell.execute(cmd);
        System.out.println(jshell.getDirTrie().getCurrent().getName());

        assertEquals(jshell.getDirTrie().getRoot(),
                jshell.getDirTrie().getCurrent());
    }
}
