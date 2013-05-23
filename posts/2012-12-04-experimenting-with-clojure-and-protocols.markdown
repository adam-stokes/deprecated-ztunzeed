Topic: "Experimenting with clojure and protocols"
Date: 2012-12-04T15:00:00Z
Category: clojure

I started messing around with some clojure code recently to see what I
could come up with in a short period of time. My main goal was to
provide some sort of overlay to adding a specific dispatch to handle
different datatypes when inserting into a database. So for my
experiment I decided to use the jdbc interface within Clojure and some
built-in function/macros to try and make light of my idea.

First I created my namespace to keep everything organized.

    (ns rosay.models
      (:require [clojure.java.jdbc :as sql]))

Next I defined a postgres database to use and already had some tables
created with a few simple constraints. I won't go into those details
but I'll show you what the connection looks like.

    (def rosay-db
      {:subprotocol "postgresql"
       :subname "//localhost/rosaydb"
       :user "adbuser"
       :password "dbpass"})

From there I defined a helper function to deal with inserting the
record into the database.

    (defn- db-insert
      [table record]
      "Inserts record based on table/record map"
      (sql/with-connection
        rosay-db
        (sql/transaction
         (sql/insert-record table record))))

All this was outlined in the relevant api documentation. From this
point I setup a protocol to hopefully help me abstract out what to do
for different datatypes I wish to store.

    ;; public interface
    (defprotocol DBFactory
      (add-item [_] "Adds item to db"))

I've defined **add-item** in order to facilitate what it is I wish to
do to each record. The records I am current concentrating on are
these:

    (defrecord Page [name description keywords frontpage client_id pages_type_id]
      DBFactory
      (add-item [_]
        (db-insert :pages {:name name
                                      :description description
                                      :keywords keywords
                                      :frontpage frontpage
                                      :client_id client_id
                                      :pages_type_id pages_type_id})))
    
    (defrecord Client [username password email domain]
      DBFactory
      (add-item [_]
        (db-insert :clients {:username username
                             :password password
                             :email email
                             :domain domain})))

With this code in place I load up my REPL and attempt to add a Client
and a Page to my database.

    rosay.server=> (use 'rosay.models)
     nil
     rosay.server=> (add-item (->Client "booyaka" "fark" "mailzer" "domain.com"))
     {:updated_on nil, :created_on #inst
     "2012-12-04T04:25:22.672462000-00:00", :email "mailzer",
     :domain "domain.com", :password "fark", :username "booyaka", :id 10}
     
     rosay.server=> (add-item (->Page "im a new page" "description of new page" "somekeywords,keywords true 10 1))
    {:updated_on nil, :created_on #inst "2012-12-04T04:41:41.716319000-00:00", :pages_type_id 1, :client_id 10, :frontpage true, :keywords "somekeywords,keywords", :description "description of new page", :name "im a new page", :id 4}

So it looked like it added my records based on the type to the correct
tables.

In summary, it was pretty easy to setup and the approach seems
straight forward to me. Although, I've created a SO post to get input
from the more experienced clojure developers on whether or not this
even makes sense. Hopefully, I'm not to far off base with attempting
to abstract out the low-level database interactions when wanting to
add some sort of dispatch-like system when adding records to a
database.

***NB*** This entire post could be completely off as I am in no-way a
seasoned clojure/lisp programmer. Recommendations/changes are always welcomed!
