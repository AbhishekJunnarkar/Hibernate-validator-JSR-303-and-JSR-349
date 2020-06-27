# Hibernate-validator-JSR-303-and-JSR-349
How and Why to use Hibernate validator JSR 303 and JSR 349 defines Bean Validation API

Hibernate Validator is reference implementation of JSR 303 and JSR 349

## Steps in implementing Server side Validation

### Step 0: (Prerequisite): No arg constructor for the Beans

In order for spring to use the binding, the spring expects a no argument constructor

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
    
### Step 2: In the Bean, add the validations
   
### Step 3: Use the validations in the controller
  
### Step 4: Display Error in the View
