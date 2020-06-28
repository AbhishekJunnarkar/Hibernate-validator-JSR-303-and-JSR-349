# Hibernate-validator-JSR-303-and-JSR-349
How and Why to use Hibernate validator JSR 303 and JSR 349 defines Bean Validation API

Hibernate Validator is reference implementation of JSR 303 and JSR 349

## Steps in implementing Server side Validation

### Step 0: (Prerequisite): No arg constructor for the Beans

In order for spring to use the binding, the spring expects a no argument constructor.

The concept is Double Binding

i.e. The bean is bound to the form and vice versa, hence called as double binding.

* This simply means if the bean is updated from backend the form will load the value and 
* If the form is loaded/updated/deleted(e.g.table row) form the front end the bean will also have the updated value

### Step 1: Model attribute or form backed Bean
  In the JSP, make the bean a model attribute
    * e.g. <form method="post" modelAttribute="todo"
Also, to be sure that the form bean is added <%@taglib uri="http://www.springframework.org/tags/form" prefix="form"%>

    <form:form method="post" modelAttribute="todo">
			  <fieldset class="form-group">
				  <label>Description : </label> <input name="desc" type="text"
					  class="form-control" required="required"/>
			  </fieldset>
			  <button type="submit" class="btn btn-success">Add</button>
		</form:form>
		
Additionally, to show the text-warning message on failure, add:
e.g. <form:errors path="desc" cssClass="text-warning" /> in the jsp 
    
### Step 2: In the Bean, add the validations
  	@Size(min = 10, message = "Enter atleast 10 characters")
	private String desc;
### Step 3: Use the validations in the controller
  @RequestMapping(value = "/add-todo", method = RequestMethod.POST)
	public String addTodo(ModelMap model, @Valid Todo todo, BindingResult result) {
		if (result.hasErrors()) {
			return "/todo";
		}
		todoService.addTodo((String) model.get("name"), todo.getDesc(), new Date(), false);
		model.put("todos", todoService.retrieveTodos((String) model.get("name")));
		return "/todo-list";// redirect:/todo-list
	}
### Step 4: Display Error in the View

![alt text](https://github.com/AbhishekJunnarkar/Hibernate-validator-JSR-303-and-JSR-349/blob/master/Hibernate%20validator%20simple%20Example01.PNG?raw=true "Validation message")

## Appendix : Default built in javax.validation.constraints

Enum Summary
Pattern.Flag | Possible Regexp flags.


Annotation Types Summary |Annotation Type Description
* AssertFalse: The annotated element must be false.
* AssertFalse.List: Defines several AssertFalse annotations on the same element.
* AssertTrue: The annotated element must be true.
* AssertTrue.List: Defines several AssertTrue annotations on the same element.
* DecimalMax:The annotated element must be a number whose value must be lower or equal to the specified maximum.
* DecimalMax.List: Defines several DecimalMax annotations on the same element.
* DecimalMin: The annotated element must be a number whose value must be higher or equal to the specified minimum.
* DecimalMin.List: Defines several DecimalMin annotations on the same element.
* Digits: The annotated element must be a number within accepted range Supported types are: BigDecimal BigInteger CharSequence byte, short, int, long, and their respective wrapper types, null elements are considered valid.

* Digits.List: Defines several Digits annotations on the same element.
* Future: The annotated element must be a date in the future.
* Future.List: Defines several Future annotations on the same element.
* Max: The annotated element must be a number whose value must be lower or equal to the specified maximum.
* Max.List:Defines several Max annotations on the same element.
* Min: The annotated element must be a number whose value must be higher or equal to the specified minimum.
* Min.List: Defines several Min annotations on the same element.
* NotNull: The annotated element must not be null.
* NotNull.List: Defines several NotNull annotations on the same element.
* Null: The annotated element must be null.
* Null.List: Defines several Null annotations on the same element.
* Past: The annotated element must be a date in the past.
* Past.List: Defines several Past annotations on the same element.
* Pattern	:The annotated CharSequence must match the specified regular expression.
* Pattern.List : Defines several Pattern annotations on the same element.
* Size:The annotated element size must be between the specified boundaries (included).
* Size.List: Defines several Size annotations on the same element.
