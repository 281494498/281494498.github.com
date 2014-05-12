---
layout: post
title: "Javascript snippet testing"
description: ""
category: remarks
tags: []
---
{% include JB/setup %}

###Simple javascript test site
    <html>
    <head>
        <title>Test Suite</title>
        <script>
    
            function assert(value, desc) {
                var li = document.createElement("li");
                li.className = value ? "pass" : "fail";
                li.appendChild(document.createTextNode(desc));
                document.getElementById("results").appendChild(li);
            }
    
            window.onload = function() {
                //fill in here
            };
        </script>
        <script type="text/javascript" src="speedTest.js"></script>
        <style>
            #results li.pass { color: green; }
            #results li.fail { color: red; }
        </style>
    </head>
    
    <body>
    <ul id="results"></ul>
    </body>
    </html>
    ----------------
###Group javascript test site
    <html>
      <head>
        <title>Group Test Suite</title>
        <script>
    
          (function() {
            var results;
            this.assert = function assert(value, desc) {
              var li = document.createElement("li");
              li.className = value ? "pass" : "fail";
              li.appendChild(document.createTextNode(desc));
              results.appendChild(li);
              if (!value) {
                li.parentNode.parentNode.className = "fail";
              }
              return li;
            };
            this.test = function test(name, fn) {
              results = document.getElementById("results");
              results = assert(true, name).appendChild(
                  document.createElement("ul"));
              fn();
            };
          })();
    
          window.onload = function() {
            test("A test.", function() {
              assert(true, "First assertion completed");
              assert(true, "Second assertion completed");
              assert(true, "Third assertion completed");
            });
            test("Another test.", function() {
              assert(true, "First test completed");
              assert(false, "Second test failed");
              assert(true, "Third assertion completed");
            });
            test("A third test.", function() {
              assert(null, "fail");
              assert(5, "pass")
            });
          };
        </script>
        <style>
          #results li.pass { color: green; }
          #results li.fail { color: red; }
        </style>
      </head>
      <body>
        <ul id="results"></ul>
      </body>
    </html>
    ----------------
###Asynchronous Test Suite
    <html>
      <head>
        <title>Asynchronous Test Suite</title>
        <script>
          (function() {
            var queue = [], paused = false, results;
            this.test = function(name, fn) {
              queue.push(function() {
                results = document.getElementById("results");
                results = assert(true, name).appendChild(
                    document.createElement("ul"));
                fn();
              });
              runTest();
            };
            this.pause = function() {
              paused = true;
            };
            this.resume = function() {
              paused = false;
              setTimeout(runTest, 1);
            };
            function runTest() {
              if (!paused && queue.length) {
                (queue.shift())();
                if (!paused) {
                  resume();
                }
              }
            }
    
            this.assert = function assert(value, desc) {
              var li = document.createElement("li");
              li.className = value ? "pass" : "fail";
              li.appendChild(document.createTextNode(desc));
              results.appendChild(li);
              if (!value) {
                li.parentNode.parentNode.className = "fail";
              }
              return li;
            };
          })();
    
    
          window.onload = function() {
            test("Async Test #1", function() {
              pause();
              setTimeout(function() {
                assert(true, "First test completed");
                resume();
              }, 1000);
            });
            test("Async Test #2", function() {
              pause();
              setTimeout(function() {
                assert(true, "Second test completed");
                resume();
              }, 1000);
            });
          };
        </script>
        <style>
          #results li.pass {
            color: green;
          }
    
          #results li.fail {
            color: red;
          }
        </style>
      </head>
      <body>
        <ul id="results"></ul>
      </body>
    </html>
