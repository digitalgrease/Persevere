<?php

/*
 * Copyright (c) 2015 Tom Gray
 */

/**
 * Defines a library function to repeatedly attempt to call a function that
 * throws an exception until it no longer throws the exception or a pre-defined
 * number of attempts has been reached.
 * 
 * @author Tom Gray
 */
class Persevere
{
    /**
     * The default maximum number of times to call the function in case of an exception.
     * 
     * @var integer
     */
    const NUMBER_OF_ATTEMPTS = 5;
    
    /**
     * Persevere with calling the given function repeatedly if it throws an
     * exception.
     * 
     * @param string  $function
     * @param array   $args
     * @param object  $object
     * @param integer $nAttempts
     * 
     * @return mixed
     * 
     * @throws Exception
     */
    public static function persevere(
        $function,
        array $args = [],
        $object = null,
        $nAttempts = self::NUMBER_OF_ATTEMPTS
    ) {
        if (!empty($args)) {
            $argString = '';
            foreach ($args as $arg) {
                $argString = $arg . ', ';
            }
            $argString = substr($argString, 0, -2);
        }
        
        // Attempt to call the function repeatedly.
        $ex = null;
        $iAttempt = 0;
        while ($iAttempt < $nAttempts) {
            try {
                return empty($object)
                    ? empty($args) ? $function() : $function($argString)
                    : empty($args) ? $object->$function() : $object->$function($argString);
            } catch (\Exception $ex) {
                ++$iAttempt;
            }
        }
        throw $ex;
    }
}
