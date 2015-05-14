
package jshell;

import java.util.ArrayList;


public class Node{
    
        private String name;
        private Node parent;
        private ArrayList <Node> children;
        private String content;
        
        /**
         * Create a Node which represents a file or directory.
         * 
         * @param parent The directory containing the directory/file (Node).
         * @param name The name of the directory/file (Node).
         */
        Node(Node parent, String name){
            this.name = name;
            this.parent = parent;
            this.children = new ArrayList();                     
        }

        /**
         * Add Node to parent's children.
         */
        public void attachNode(){
            this.parent.getChildren().add(this);
            
        }
        /**
         * Return the name of a file/directory (Node).
         * @return String The name of a file/directory (Node).
         */
        public String getName(){
            return this.name;
        }
        
        /**
         * Return the contents of a Node - null if Node is a directory.
         * @return String The contents of a Node.
         */
        public String getContent(){
            return this.content;
        }
        /**
         * Sets the content of a Node; used for 'File' objects.
         * @param content The String content of the 'file' (Node).
         */
        public void setContent(String content){
            
            this.content = content;
                        
        }
        
        /**
         * Return a list of the children of node 
         * (null unless node is directory).
         * @return ArrayList The child directories/files of directory (node).
         */
        public ArrayList getChildren(){
            return this.children;
        }
        /**
         * Return the directory (node) that points to the node (directory/file).
         * @return Node The directory (node) in which node is held.
         */
        public Node getParent(){
            return this.parent;
        }

    }