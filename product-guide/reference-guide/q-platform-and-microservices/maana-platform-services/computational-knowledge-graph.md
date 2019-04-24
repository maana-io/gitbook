# Computational Knowledge Graph

## The Computational Knowledge Graph

The Maana Computational Knowledge Graph™ \(CKG\) is a network of models that optimize specific operations and decisions flows, by providing recommendations through AI-Driven Applications. This unique technology eliminates the need to move data, and enables creation of thousands of models at scale, through the re-usability of models across the enterprise.

{% hint style="info" %}
**Example**:  A working, real-world example of a CKG might be a Knowledge Graph that contains a network of models describing the oil wells dug in the Gulf of Mexico during the last 50 years-including companies, people, equipment and activities involved, etc.
{% endhint %}

### CKG Key Components

<table>
  <thead>
    <tr>
      <th style="text-align:left"><b>Term</b>
      </th>
      <th style="text-align:left"><b>Description</b>
      </th>
      <th style="text-align:left"><b>Example</b>
      </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Kinds</td>
      <td style="text-align:left">Kinds are Concepts.</td>
      <td style="text-align:left">Examples: People, Ships, Oil Wells, Invoices&#x202F;</td>
    </tr>
    <tr>
      <td style="text-align:left">Fields/Entities</td>
      <td style="text-align:left">Entities are properties within a certain Concept.</td>
      <td style="text-align:left">Such as entities related to the People concept: age, sex, height, weight,
        etc.</td>
    </tr>
    <tr>
      <td style="text-align:left">Instances</td>
      <td style="text-align:left">&#x202F;A particular set of values for Entities within a Concept.</td>
      <td
      style="text-align:left">Such as: Paul, 40yrs old, male, 6&apos;, 180 pounds</td>
    </tr>
    <tr>
      <td style="text-align:left">Values</td>
      <td style="text-align:left">A particular size, measure, number of an Entity.</td>
      <td style="text-align:left">Example of a value: 40Example of an instance: Paul, 40yrs old, male, 6&apos;,
        180pounds</td>
    </tr>
    <tr>
      <td style="text-align:left">Relations</td>
      <td style="text-align:left">Connections/dependencies that can be established between fields belonging
        to different Kinds.</td>
      <td style="text-align:left">A Kind describing an oil well may contain a field of a type of a String
        showing the name of the company operating that well. That field has a relation
        with the Kind containing Company Names.</td>
    </tr>
    <tr>
      <td style="text-align:left">Micro-service</td>
      <td style="text-align:left">Micro-services are small in size, independently deployable and easy to
        replace.</td>
      <td style="text-align:left">
        <p>Example Micro-services:
          <br /> <b>io.maana.nlp</b>  <b>service </b>(Natural Language Processing-NLP)</p>
        <p><b>io.maana.ner service (</b>Named Entity Recognition-NER)</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">Bot Action</td>
      <td style="text-align:left">Micro-services can emit events (act as publishers) which trigger automatic
        action(s) from other services (acting as subscribers) that react to those
        events.</td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left">String</td>
      <td style="text-align:left">any arbitrary length character sequence and is the most generic representation
        (i.e. it has little meaning)</td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>{% hint style="info" %}
**Knowledge Accelerator Tip:** Check out our short Tutorial \(link to Tutorial doc\) with a specific, dataset-driven example on how you can create and explore a CKG. It will help you move much faster when you will create the first CKG from your own data!
{% endhint %}

### 

| \[TBD\] @Darrell |
| :--- |


