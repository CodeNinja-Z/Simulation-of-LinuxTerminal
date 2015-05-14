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
 * @author baxx
 */
public class NodeTest {
    
    public NodeTest() {
    }

    @BeforeClass
    public static void setUpClass() {
    }

    @AfterClass
    public static void tearDownClass() {
    }
    
    @Before
    public void setUp() {
    }
    
    @After
    public void tearDown() {
    }

    /**
     * Test of getName method, of class Node.
     */
    @Test
    public void testGet_name() {
        System.out.println("get_name");
        Node instance = new Node(null,"node");
        String expResult = "node";
        String result = instance.getName();
        assertEquals(expResult, result);
}

    /**
     * Test of getContent method, of class Node.
     */
    @Test
    public void testGet_content() {
        System.out.println("get_content");
        Node instance = new Node(null,"node");
        String expResult = null;
        String result = instance.getContent();
        assertEquals(expResult, result);

    }

   /**
     * Test of getContent method, of class Node.
     */
    @Test
    public void testSet_content() {
        System.out.println("set_content");
        Node instance = new Node(null,"node");
        String Content = "Node Content";
        instance.setContent(Content);
        String result = instance.getContent();
        assertEquals(Content, result);

    }
    
    
    
    /**
     * Test of get_child method, of class Node.
     */
    @Test
    public void testGet_children() {
        System.out.println("get_children");
        Node Node1 = new Node(null,"node1");
        ArrayList expResult1 = new ArrayList();
        ArrayList result1 = Node1.getChildren();
        assertEquals(expResult1, result1);
        
        Node Node2 = new Node(Node1,"node2");
        Node2.attachNode();
        
        ArrayList expResult2 = new ArrayList();
        expResult2.add(Node2);
        ArrayList result2 = Node1.getChildren();
        assertEquals(expResult2, result2);
}

    /**
     * Test of getParent method, of class Node.
     */
    @Test
    public void testGet_parent() {
        System.out.println("get_parent");
        Node Node1 = new Node(null,"node1");
        Node expResult = null;
        Node result = Node1.getParent();
        assertEquals(expResult, result);
        
        Node Node2 = new Node(Node1,"node2");
        Node result2 = Node2.getParent();
        assertEquals(Node1, result2);

    }
}
