package client;

import java.net.MalformedURLException;
import java.net.URL;
import java.util.ArrayList;
import java.util.List;

import javax.xml.namespace.QName;
import javax.xml.ws.Holder;
import javax.xml.ws.Service;

import introsde.assignment.soap.ws.HealthMeasureHistory;
import introsde.assignment.soap.ws.People;
import introsde.assignment.soap.ws.Person;
import introsde.assignment.soap.ws.Person.CurrentHealth;


public class PeopleClient{
	private URL url = null;
	private Service service = null;
	private People people = null;
	private QName qname = null;

	private int first_person_id = -1;
	private int last_person_id = -1;
	HealthMeasureHistory measure_element_first_id = null;

	public PeopleClient(String input_url) throws MalformedURLException{
		url = new URL(input_url);
		//1st argument service URI, refer to wsdl document above
		//2nd argument is service name, refer to wsdl document above
		qname = new QName("http://ws.soap.assignment.introsde/", "PeopleService");
		service = Service.create(url, qname);

		people = service.getPort(People.class);
	}


	private void readPersonList() {
		responseTemplate(1, "readPersonList");
		System.out.println("RESPONSE: ");
		List<Person> p_list = people.getPeopleList();
		first_person_id = p_list.get(0).getIdPerson();
		last_person_id = p_list.get(p_list.size()-1).getIdPerson();
		for(Person p: p_list){
			printPerson(p);
		}
	}

	public Person readPerson(){
		responseTemplate(2, "readPerson");
		System.out.println("REQUEST: ");
		System.out.println("id: "+first_person_id);
		Person p = people.readPerson(first_person_id);
		System.out.println(" ");
		System.out.println("RESPONSE: ");
		printPerson(p);
		return p;
	}

	private void updatePerson() {
		responseTemplate(3, "updatePerson");
		String name = "Pippo";
		System.out.println("Person #"+first_person_id+" before the update:");
		Person p = people.readPerson(first_person_id);
		printPerson(p);
		p.setCurrentHealth(null);
		p.setFirstname(name);
		System.out.println(" ");
		System.out.println("REQUEST: ");
		System.out.println("id: "+first_person_id);
		System.out.println("firstname: "+ name);
		System.out.println(" ");

		int response = people.updatePerson(p);
		System.out.println("RESPONSE:");
		String res = (response == 0) ? "OK" : "ERROR";
		System.out.println("code: "+response+" "+res );
		System.out.println(" ");
		System.out.println("Person #"+first_person_id+" after the update:");
		Person p1 = people.readPerson(first_person_id);
		printPerson(p1);
	}

	private void createPerson() {
		responseTemplate(4, "createPerson");
		Person p = new Person();
		p.setFirstname("Chuck");
		p.setLastname("Norris");
		p.setBirthdate("1945-01-01");
		List<HealthMeasureHistory> measure = new ArrayList<>();
		HealthMeasureHistory m = new HealthMeasureHistory();
		m.setMeasureType("height");
		m.setMeasureValue("180");
		m.setMeasureValueType("Int");
		m.setDateRegistered("2015-01-01");
		measure.add(m);
		System.out.println(" ");
		System.out.println("REQUEST: ");
		printPerson(p);
		printMeasure(m);
		int idPerson = people.createPerson(p, measure);
		System.out.println(" ");
		System.out.println("RESPONSE:");
		System.out.println("id created person: "+idPerson);
		System.out.println(" ");
		System.out.println("Created Person");
		Person person = people.readPerson(idPerson);
		printPerson(person);
	}

	private void deletePerson() {
		responseTemplate(5, "deletePerson");
		System.out.println("REQUEST: ");
		System.out.println("id: "+last_person_id);
		Holder<Integer> id = new Holder<Integer>(last_person_id);
		people.deletePerson(id);
		System.out.println(" ");
		System.out.println("RESPONSE:");
		System.out.println("readPerson("+last_person_id+"): "+people.readPerson(last_person_id));	
	}

	private void readPersonHistory() {
		responseTemplate(6, "readPersonHistory");
		String measureType = "weight";
		System.out.println("REQUEST: ");
		System.out.println("id: "+first_person_id);
		System.out.println("measureType: "+measureType);
		System.out.println(" ");
		List<HealthMeasureHistory> history = people.readPersonHistory(first_person_id, measureType);
		for(HealthMeasureHistory m: history){
			printMeasure(m);
		}
	}

	private void readMeasureTypes() {
		responseTemplate(7, "readMeasureTypes");
		List<String> measureTypes = people.readMeasureTypes();
		System.out.println(" ");
		System.out.println("RESPONSE:");
		for(String m: measureTypes){
			System.out.println(m);
		}
	}

	private void readPersonMeasure() {
		responseTemplate(8, "readPersonMeasure");
		HealthMeasureHistory measure_first_person = people.readPerson(first_person_id).getCurrentHealth().getMeasure().get(0);
		String measureType = measure_first_person.getMeasureType();
		int mid = measure_first_person.getMid();
		System.out.println("REQUEST: ");
		System.out.println("id: "+first_person_id);
		System.out.println("measureType: "+measureType);
		System.out.println("mid: "+mid);
		System.out.println(" ");
		System.out.println("RESPONSE:");
		measure_element_first_id = people.readPersonMeasure(first_person_id, measureType, mid);
		printMeasure(measure_element_first_id);
	}



	private void savePersonMeasure() {
		responseTemplate(9, "savePersonMeasure");
		HealthMeasureHistory measure = new HealthMeasureHistory();
		measure.setMeasureType("weight");
		measure.setMeasureValue("100");
		measure.setMeasureValueType("Int");
		measure.setDateRegistered("2015-10-12");
		System.out.println("REQUEST: ");
		System.out.println("id: "+first_person_id);
		printMeasure(measure);
		int response = people.savePersonMeasure(first_person_id, measure);
		System.out.println(" ");
		System.out.println("RESPONSE:");
		String res = (response != -1) ? "OK" : "ERROR";
		System.out.println("id: "+response+" "+res );
		System.out.println(" ");
		printMeasure(people.readPersonMeasure(first_person_id, measure.getMeasureType(), response));
	}


	private void updatePersonMeasure() {
		responseTemplate(10, "updatePersonMeasure");
		System.out.println("REQUEST: ");
		System.out.println("id: "+first_person_id);
		printMeasure(measure_element_first_id);
		measure_element_first_id.setMeasureValue("75");
		System.out.println(" ");
		System.out.println("RESPONSE:");
		Holder<HealthMeasureHistory> measure = new Holder<HealthMeasureHistory>(measure_element_first_id);
		people.updatePersonMeasure(first_person_id, measure);
		printMeasure(people.readPersonMeasure(first_person_id,
				measure_element_first_id.getMeasureType(),
				measure_element_first_id.getMid()));
	}

	public void printPerson(Person person) {
		System.out.println("******************");
		System.out.println("id       : "+ person.getIdPerson());
		System.out.println("firstname: "+ person.getFirstname());
		System.out.println("lastname : "+ person.getLastname());
		System.out.println("birthdate : "+ person.getBirthdate());
		if(person.getCurrentHealth() != null){
			printCurrentHealth(person.getCurrentHealth());
		}
	}

	public void printCurrentHealth(CurrentHealth ch) {
		List<HealthMeasureHistory> list_measure = ch.getMeasure();
		for(HealthMeasureHistory m: list_measure){
			printMeasure(m);
		}
	}
	public void printMeasure(HealthMeasureHistory m){
		System.out.println("-----------");
		System.out.println("id               : "+ m.getMid());
		System.out.println("dateRegistered   : "+ m.getDateRegistered());
		System.out.println("measureType      : "+ m.getMeasureType());
		System.out.println("value            : "+ m.getMeasureValue());
		System.out.println("measureValueType : "+ m.getMeasureValueType());
	}

	public void responseTemplate(int req, String method){
		System.out.println(" ");
		System.out.println("===========================================================================");
		System.out.println("Request #"+req+": "+method);
		System.out.println(" ");
	}


	public static void main(String[] args) throws Exception {
		if (args.length < 1)
			System.out.println("Error: insert server url");
		else{

			try {
				PeopleClient c = new PeopleClient(args[0]);
				c.readPersonList();	//Method 1
				c.readPerson(); 	//Method 2
				c.updatePerson();	//Method 3
				c.createPerson();	//Method 4
				c.deletePerson();	//Method 5
				c.readPersonHistory(); //Method 6
				c.readMeasureTypes(); //Method 7
				c.readPersonMeasure(); //Method 8
				c.savePersonMeasure(); //Method 9
				c.updatePersonMeasure(); //Method 10
				
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	}    
}
