<frontmatter>
title: CS3282 - {{ year }} Batch
pageNav: 2
</frontmatter>

# CS3282 - {{ year }} Batch

{% set projects = [
    {name: 'MarkBind', students: [
        ['CHAN GER TECK', 'gerteck', 'A1', 'B1', 'C1']
    ]},
    {name: 'Open', students: [
        ['LOH ZE QING, NORBERT', 'NorbertLoh', 'A1', 'B1', 'C1'],
        ['MISRA ADITYA', 'MadLamprey', 'A1', 'B1', 'C1'],
        ['SOH ZHENG YANG, MARCUS', 'HollaG', 'A1', 'B1', 'C1']
    ]},
    {name: 'TEAMMATES', students: [
        ['CHING MING YUAN', 'mingyuanc', 'A1', 'B1', 'C1'],
        ['DHIRAPUTTA PATHAMA TENGARA', 'DhiraPT', 'A1', 'B1', 'C1']
    ]}
] %}

{% for project in projects %}
**{{ project.name }}:**
{% for student in project.students %}* [{{ student[0] }}](#{{ student[0] | lower | replace(' ', '-') | replace(',', '')}})
{% endfor %}
{% endfor %}

{% for project in projects %}
# {{ project.name }}
  {% for student in project.students %}

<include src="students/{{ student[1] }}/studentInfo.md" boilerplate >
  <span id="name">{{ student[0] }}</span>
  <span id="folder">{{ student[1] }}</span>
  <span id="mod">cs3282</span>
</include>
  {% endfor %}
{% endfor %}
