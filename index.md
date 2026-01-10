<frontmatter>
title: CS3281&2 - {{ year }} Batch
pageNav: 2
</frontmatter>

# CS3281 - {{ year }} Batch

{% set projects = [
    {name: 'Git-Mastery', students: [
        ['DESMOND WONG HUI SHENG', 'desmondwong1215'],
        ['GOYAL VIKRAM', 'VikramGoyal23'],
        ['JOVAN NG CHENGEN', 'jovnc'],
        ['LOH JIA XIN', 'jiaxinnns'],
        ['SAN MUYUN', 'SAN-MUYUN']
    ]},
    {name: 'MarkBind', students: [
        ['CHUA JIA CHEN THADDAEUS', 'MoshiMoshiMochi'],
        ['HARVINDER ARJUN SINGH S/O SUKHWANT SINGH', 'Harjun751'],
        ['HON YI HAO', 'yihao03']
    ]},
    {name: 'Open', students: [
        ['DALLAS LIM JUIN LOON', 'BladerX11'],
        ['GABRIEL MARIO ANTAPUTRA', 'thegrimbee']
    ]},
    {name: 'RepoSense', students: [
        ['CHEN YIZHONG', 'yizhong187'],
        ['HALDAR ASHMITA', 'ashmitahaldar'],
        ['YU LETIAN', 'FisherSkyi']
    ]},
    {name: 'TEAMMATES', students: [
        ['AARON TOH YINGWEI', 'AaronToh'],
        ['FLORIAN VIOREL TANELY', 'iZUMi-kyouka'],
        ['KOH WEE JEAN', 'WeeJean'],
        ['PHOEBE YAP XIN HUI', 'PhoebeY05'],
        ['SARIPALLI BHAGAT SAI REDDY', 'Nsohko'],
        ['YONG JUN XI', 'TobyCyan']
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
  <span id="mod">cs3281</span>
</include>
  {% endfor %}
{% endfor %}
