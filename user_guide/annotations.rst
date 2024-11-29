Annotations
===========

Historically Behat used doc-block annotations instead of attributes to define steps, hooks and
transformations in PHP contexts. These annotations are still available for now, and you can use them instead
of PHP attributes in your projects - however they will likely be deprecated and removed in the future.

Step Annotations
----------------

Here is an example of how you can define your steps using annotations:

.. code-block:: php

    // features/bootstrap/FeatureContext.php

    use Behat\Behat\Context\Context;

    class FeatureContext implements Context
    {
        /*
         * @Given we have some context
         */
        public function prepareContext()
        {
            // do something
        }

        /*
         * @When an :event occurs
         */
        public function onEvent(string $event)
        {
            // do something
        }

        /*
         * @Then something should be done
         */
        public function checkOutcomes()
        {
            // do something
        }
    }

The pattern that you would include as an argument to the step attribute should be listed here
after the annotation, separated by a space

Hook Annotations
----------------

Here is an example of how you can define your hooks using annotations:

.. code-block:: php

    // features/bootstrap/FeatureContext.php

    use Behat\Behat\Context\Context;
    use Behat\Testwork\Hook\Scope\BeforeSuiteScope;
    use Behat\Behat\Hook\Scope\AfterScenarioScope;

    class FeatureContext implements Context
    {
        /*
         * @BeforeSuite
         */
        public static function prepare(BeforeSuiteScope $scope)
        {
        }

        /*
         * @AfterScenario @database
         */
        public function cleanDB(AfterScenarioScope $scope)
        {
        }
    }

Transformation Annotations
--------------------------

Here is an example of how you can define your transformations using annotations:

.. code-block:: php

    // features/bootstrap/FeatureContext.php

    use Behat\Behat\Context\Context;

    class FeatureContext implements Context
    {
        /*
         * @Transform /^(\d+)$/
         */
        public function castStringToNumber($string)
        {
            return intval($string);
        }
    }

Existing code
-------------

Even though annotations are still available, they will probably be deprecated and eventually removed in the future.
Therefore, we do not recommend using annotations for new projects. If your current project uses annotations, we
recommend that you refactor your code to use PHP attributes instead. This can be done manually but you should be able
to use the search and replace capabilities of your IDE to do this in a more automated way.

Alternatively you may want to use a tool like `Rector`_ which can do automated refactoring of your code. Rector 2.0
includes a rule that allows you to automatically convert any doc-block annotations to the corresponding attributes.
To use it for your Behat contexts, add the following option to your Rector configuration:

.. code-block:: php

    ->withAttributesSets(behat: true)

.. _`Rector`: https://github.com/rectorphp/rector

