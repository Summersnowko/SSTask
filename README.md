# SSTaskpackage softServeTask;
import java.util.*;

public class Main {
	public static abstract class Worker{
		protected int id;
		protected String name;
		
		public int getID(){
			return id;
		}
		public String getName(){
			return name;
		}
		
		abstract double getMonthPay();
		
		private Worker(int id, String name){
			this.id = id;
			this.name = name;
					
		}
		
		
	}
	public static class Employee extends Worker{
		private double monthAveragePay;
		
		@Override
		public double getMonthPay(){
			return monthAveragePay;
		}
		
		public Employee(int id, String name, double monthAveragePay){
			super(id, name);
			this.monthAveragePay = monthAveragePay;
		}
		
		@Override
		public String toString(){
			return "Employee id: " + super.id + ". Employee name is " + super.name + ", " + 
			super.name + " month average pay is " + monthAveragePay + "$";
			
		}
		
		
	}
	public static class Contractor extends Worker{
		private double hourAveragePay;
		public static final double COUNT_OF_WORKING_HOURS = 8 * 20.8;
		
		public Contractor(int id, String name, double hourAveragePay){
			super(id, name);
			this.hourAveragePay = hourAveragePay;
		}

		@Override
		double getMonthPay() {
			double tmp = hourAveragePay * COUNT_OF_WORKING_HOURS;
			return tmp;
		}
		@Override
		public String toString(){
			return "Contractor id: " + super.id + ". Contractor name is " + super.name + ", " + 
		    super.name + " month average pay is " + getMonthPay() + "$";
		}
	}
	public static class PaymentOrNameComparator implements Comparator<Worker>{
		@Override
		public int compare(Worker a, Worker b){
			if(a.getMonthPay() < b.getMonthPay()) return -1;
			if(a.getMonthPay() > b.getMonthPay()) return 1;
			else return a.getName().compareTo(b.getName());
		
		}
		
	}
	public static void main(String[] args){
		List<Worker> list= new ArrayList<Worker>();
		list.add(new Employee(10, "Leonard", 1700));
		list.add(new Contractor(20, " Sheldon", 11.3));
		list.add(new Contractor(21, "Govard", 9.14));
		list.add(new Contractor(22, "Rajesh", 10.3));
		list.add(new Employee(11, "Amy", 1650));
		list.add(new Employee(12, "Bernadeth", 1900));
		
		Collections.sort(list, new PaymentOrNameComparator());
		
		for(Worker obj : list){
			System.out.println(obj);
		}
		System.out.println("===================================================================");
		for(int i = list.size(); i > list.size() - 3; i--){
			System.out.print(list.get(i-1).getID() + " ");
		}
		System.out.println();
	}

}
