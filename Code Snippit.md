using Microsoft.AspNetCore.Mvc.ApplicationModels;
using System.ComponentModel.DataAnnotations;
using System.Security.Cryptography.X509Certificates;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace TicketCounter.Models
{
    public class Stack
    {
        // Members
        private int top;// top of stack
        private int next;//next item in stack
        private int maxSize;
        private int stackSize;
        private int?[] stackItems;

        public Stack()
        {
            this.maxSize = 5;
            this.stackSize = -1;
            this.top = -1;
            this.next = -1;
            this.stackItems = new int?[maxSize];
        }

        public Stack(int maxSize)
        {
            this.maxSize = maxSize;
            this.stackSize = 0;
            this.top = -1;
            this.next = 0;
            this.stackItems = new int?[maxSize];
        }

        public bool IsFull()
        {
            return top == maxSize;
        }

        public bool IsEmpty()
        {

            return top == -1;

        }

        public int Size()
        {

            return stackSize;
        }

        public int? Peek()
        {
            if (!this.IsEmpty())
                return stackItems[top];
            throw new Exception();

            // if the stack is not empty this returns the top of the stack
        }


        public int? Pop()
        {
            if (!this.IsEmpty())
            {
                int? item = stackItems[top];
                int index = top;
                if (index == -1)
                {
                    throw new Exception();
                }
                top = -1;
                for (int i = index; i < this.next - 1; i++)
                {
                    this.stackItems[i] = this.stackItems[i + 1];
                }
                this.stackSize--;
                this.next--;

                return item;
            }
            else
            {
                throw new Exception();
            }
        }
        // if the stack is not empty this removes the value from the top of the list and returns it


        public void Push(int? item)
        {
            if (this.IsFull())
                throw new Exception();
            else
            {
                this.top++;
                this.stackItems[this.top] = item;
                this.next++;

            }

            this.stackSize++;

            // if the stack is not already full this will add a new value to the stack
        }

        public string PrintStackUp()
        {
            string stackString = "";
            for (int i = 0; i < this.stackSize; i++)
            {
                stackString = stackString + this.stackItems[i] + "\n";
            }
            return stackString;
        }
        //returns the stack as a string
    }

    class Node
    {
        //represents name
        public string sData;
        // represents rank
        public int iData;
        // right subtree
        public Node right;
        // left subtree
        public Node left;
    }
    class Tree
    {
        //Insert method
        public Node Insert(Node root, string svalue, int ivalue)
        {
            if (root == null)
            {
                root = new Node();
                root.sData = svalue;
                root.iData = ivalue;
            }
            else if (ivalue < root.iData)
            {
                root.left = Insert(root.left, svalue, ivalue);
            }
            else
            {
                root.right = Insert(root.right, svalue, ivalue);
            }
            return root;
        }
        //inserts new values into the tree
        public object Search(object ielement, object selement, Node root)
        {
            Node current = root;
            if (current == null)
                return "Data not found";
            if (Convert.ToInt32(ielement) == Convert.ToInt32(current.iData) &&
            Convert.ToString(selement) == current.sData)
                return ielement + " " + selement;
            if (Convert.ToInt32(ielement) < Convert.ToInt32(current.iData) &&
            Convert.ToString(selement) != current.sData)
                return Search(ielement, selement, current.left);
            else
                return Search(ielement, selement, current.right);
        }
        //searches the tree for a sepcifc value


    }
    public class TicketSubmissionModel
    {
    

        [Required(ErrorMessage = "Please enter the customers name.")]
        
        public string? VenueName { get; set; }

        [Required(ErrorMessage = "Please enter how many tickets were ordered.")]
        public int TicketsBought { get; set; }

        [Required(ErrorMessage = "Please enter the ticketID to be punched.")]
        public int? TicketID { get; set; }

  
        public int? CalculateTotal()
        {
            //insert the total tickets into tree
            Node root = null;
            int ticketID = 1;
            Tree tickets = new Tree();

            for (int i = 0; i <= TicketsBought; i++)
            {
                tickets.Insert(root, VenueName, ticketID);
                ticketID++;

            }

            //find ticket to be punched and add it to the stack

            tickets.Search(VenueName, TicketID, root);


            Stack ticketsPunched = new Stack(TicketsBought);

            ticketsPunched.Push(TicketID);


            return ticketsPunched.Size();
        }
    }
}

