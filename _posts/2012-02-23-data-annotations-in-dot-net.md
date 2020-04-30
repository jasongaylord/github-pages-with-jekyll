---
title: "Using Data Annotations in the .NET Framework"
author: 
  display_name: "Jason Gaylord"
  email: "jason@jasongaylord.com"
cloudscribe_id: "9010b05a-a27a-4aa3-9008-d4992b901377"
cloudscribe_path: "/Blog/data-annotations-in-dot-net"
permalink: /Blog/data-annotations-in-dot-net
date: 2012-02-23
categories: Archive
tags: 
---

Starting with .NET 4 or MVC3, a developer could use a data annotation on a property to force data validation. This is extremely powerful especially for MVC developers. The same data annotations can also be used when building custom modules for Orchard CMS.

The annotations built into the framework include the following:

*   <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">Required</span>– Allows you to mark a property as being required.

*   <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">StringLength</span>– Allows a maximum string length to be specified for a property.

*   <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">Range</span>– Validates the value of the specified property is between a range of values.

*   <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">RegularExpression</span> – Allows you to specify a regular expression to validate the content against. A comprehensive list of regular expressions can be found at [http://regexlib.com/](http://jasong.us/wzAjYJ "http://jasong.us/wzAjYJ").



In addition to these above, custom annotations can be built by inheriting from the base class <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">ValidationAttribute</span>.

An example of a custom data annotation is shown below. This sample asks for a start and an end date to be specified as strings. The assumption is that these strings will be in a correct date format. A property value will be specified as a string. The property value must be between the two dates specified.

public class DateRange : System.ComponentModel.DataAnnotations.ValidationAttribute
{
    public string StartDate { get; set; }
    public string EndDate { get; set; }

    public DateRange() {
        this.StartDate = new DateTime(1900, 1, 1).ToString();
        this.EndDate = new DateTime(2099, 1, 1).ToString();
    }

    public override bool IsValid(object value) {
        var valueToString = value as string;
            
        if (!string.IsNullOrEmpty(valueToString)) {
            DateTime dateTimeResult;
                
            if (DateTime.TryParse(valueToString, out dateTimeResult)) {
                return ((dateTimeResult >= DateTime.Parse(this.StartDate)) && (dateTimeResult <= DateTime.Parse(this.EndDate)));
            }

            return false;
        }
        return true;
    }
}

Notice that in the code snippet above, I’m allowing null or empty strings to be passed in. Keep in mind that the <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">Required</span> annotation already checks for nulls or empty strings.

To use the <span style="font-family: consolas; font-size: x-small;" size="2" face="Consolas">DateRange</span> annotation, simply add it to a property in the model like below:

[DateRange(StartDate="1/1/2012", EndDate="12/31/2012", ErrorMessage="The date must be during the 2012 calendar year.")]
public string EventDate { get; set; }

Additional data annotations can be downloaded from a project started by [Scott Kirkland](http://jasong.us/x6XWbz) at [http://dataannotationsextensions.org/](http://jasong.us/yZqbAt "http://jasong.us/yZqbAt").

[CodeProject](http://www.codeproject.com)
