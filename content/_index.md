---
# Leave the homepage title empty to use the site title
title:
date: 2022-10-24
type: landing

sections:
  - block: hero
    content:
      # Brand wordmark rendered as the hero <h1>. Only the lowercase "i" is
      # the theme red; screen readers still read the whole word "DANiLab".
      wordmark: 'DAN<span class="home-hero__i">i</span>Lab'
      fullname: Dynamics, Astronautics & Neural Intelligence Lab
      headline: Physical AI for robotics, manufacturing and space
      text: |
        DANiLab develops intelligent systems that understand, predict and act in the physical world. Our research combines world models, vision-language-action models and autonomous control for robotics, manufacturing and space missions.
      image:
        filename: danilab-banner.jpg
        alt: Illustration of the DANiLab team with robotic systems in a laboratory
      cta:
        url: ./publication/
        label: Explore our research
      cta_alt:
        url: ./people/
        label: Meet the team
                                              
  - block: markdown
    content:
      title: Research Areas
      text: |
        <div class="row research-areas">
        <div class="col-md-6 mb-4 mb-md-0 d-flex">

        <div class="research-area">

        ## Physical AI

        Developing intelligent systems that perceive, reason, learn and act in the physical world.

        <div class="research-area__topics">
        <span class="research-area__tag">World Models</span>
        <span class="research-area__tag">Vision-Language-Action</span>
        <span class="research-area__tag">Spatial Intelligence</span>
        <span class="research-area__tag">Robot Learning</span>
        <span class="research-area__tag">Human-Robot Collaboration</span>
        <span class="research-area__tag">Agentic AI</span>
        </div>

        </div>

        </div>
        <div class="col-md-6 d-flex">

        <div class="research-area">

        ## Space Robotics &amp; Autonomous Systems

        Developing intelligent autonomy for spacecraft, robotic missions and in-space servicing, assembly and manufacturing.

        <div class="research-area__topics">
        <span class="research-area__tag">Space Mission Autonomy</span>
        <span class="research-area__tag">Spacecraft GNC</span>
        <span class="research-area__tag">ISAM</span>
        <span class="research-area__tag">In-Orbit Servicing</span>
        <span class="research-area__tag">Rendezvous and Manipulation</span>
        </div>

        </div>

        </div>
        </div>
    design:
      columns: '1'

  - block: collection
    content:
      title: Latest News
      subtitle:
      text:
      count: 3
      filters:
        author: ''
        category: ''
        exclude_featured: false
        publication_type: ''
        tag: ''
      offset: 0
      order: desc
      page_type: post
    design:
      view: newscard
      columns: '1'

  - block: markdown
    content:
      title: Work With Us
      text: |
        <div class="work-with-us">

        We welcome enquiries from prospective PhD students, postdoctoral researchers, visiting researchers and collaborators whose interests align with our work in physical AI, robotics and autonomous space systems.

        {{% cta cta_link="./contact/" cta_text="Join DANiLab" %}}

        </div>
    design:
      columns: '1'

  - block: markdown
    content:
      title: Selected Projects and Funders
      subtitle:
      text: |
        <div class="row justify-content-center">
        <div class="col-6 col-md-3 mb-4 d-flex">

        <div class="funder">
        <div class="funder__logo">

        {{< figure src="funders/uksa-logo.png" alt="UK Space Agency" class="funder-logo" lightbox="false" >}}

        </div>

        <div class="funder__caption">PI — NSIP-2 ISPARK with TWI Ltd<br>PI (Leicester) — NSTP PLATOR with Surrey Space Centre</div>

        </div>

        </div>
        <div class="col-6 col-md-3 mb-4 d-flex">

        <div class="funder">
        <div class="funder__logo">

        {{< figure src="funders/esa-logo.png" alt="European Space Agency" class="funder-logo" lightbox="false" >}}

        </div>

        <div class="funder__caption">ESA/NASA Mars Sample Return DWI Project E/019A-02R — MSR SRP E3P2</div>

        </div>

        </div>
        <div class="col-6 col-md-3 mb-4 d-flex">

        <div class="funder">
        <div class="funder__logo">

        {{< figure src="funders/ukri-epsrc-logo.png" alt="UKRI EPSRC" class="funder-logo" lightbox="false" >}}

        </div>

        <div class="funder__caption">Co-I — <a href="https://digitalmetal-cdt.ac.uk/">EPSRC Centre for Doctoral Training in Digital Transformation of Metals Industry</a></div>

        </div>

        </div>
        <div class="col-6 col-md-3 mb-4 d-flex">

        <div class="funder">
        <div class="funder__logo funder__logo--tall">

        {{< figure src="funders/agentic-6g-logo.png" alt="Agentic-6G" class="funder-logo" lightbox="false" >}}

        </div>

        <div class="funder__caption">Co-I — Agentic-6G Autonomous multi-agent agentic AI system for 6G networks</div>

        </div>

        </div>
        </div>
    design:
      columns: '1'

  # NOTE: "Latest Preprints" collection removed until publications are imported
  # (BibTeX import is deferred). With no publications it rendered an empty
  # heading. Re-add a `block: collection` with `view: citation` when ready.
---
