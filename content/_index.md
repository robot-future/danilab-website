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
      view: compact
      columns: '1'

  - block: markdown
    content:
      title:
      subtitle:
      text: |
        <div class="row text-center align-items-start">
        <div class="col-md-6 mb-4 mb-md-0">

        We're looking for motivated students and researchers to work on robotics, embodied intelligence, and autonomous systems.

        {{% cta cta_link="./contact/" cta_text="Join the lab →" %}}

        </div>
        <div class="col-md-6">

        DANiLab is a growing research group led by Dr Daniel Hao, with PhD researchers and collaborators working on AI, robotics, and autonomous systems.

        {{% cta cta_link="./people/" cta_text="Meet the team →" %}}

        </div>
        </div>
    design:
      columns: '1'

  - block: markdown
    content:
      title: Research Funders
      subtitle:
      text: |
        <div class="row text-center">
        <div class="col-6 col-md-3 mb-4">
        <div class="funder-logo-cell">

        {{< figure src="funders/uksa-logo.png" alt="UK Space Agency" class="funder-logo" lightbox="false" >}}

        </div>

        <small>PI — NSIP-2 ISPARK with TWI Ltd; PI (Leicester) — NSTP PLATOR with Surrey Space Centre</small>

        </div>
        <div class="col-6 col-md-3 mb-4">
        <div class="funder-logo-cell">

        {{< figure src="funders/esa-logo.png" alt="European Space Agency" class="funder-logo" lightbox="false" >}}

        </div>

        <small>ESA/NASA Mars Sample Return DWI Project E/019A-02R — MSR SRP E3P2</small>

        </div>
        <div class="col-6 col-md-3 mb-4">
        <div class="funder-logo-cell">

        {{< figure src="funders/ukri-epsrc-logo.png" alt="UKRI EPSRC" class="funder-logo" lightbox="false" >}}

        </div>

        <small>Co-I — EPSRC Centre for Doctoral Training in Digital Transformation of Metals Industry</small>

        </div>
        <div class="col-6 col-md-3 mb-4">
        <div class="funder-logo-cell">

        {{< figure src="funders/agentic-6g-logo.png" alt="Agentic-6G" class="funder-logo funder-logo--tall" lightbox="false" >}}

        </div>

        <small>Co-I — Agentic-6G Autonomous multi-agent agentic AI system for 6G networks</small>

        </div>
        </div>
    design:
      columns: '1'

  # NOTE: "Latest Preprints" collection removed until publications are imported
  # (BibTeX import is deferred). With no publications it rendered an empty
  # heading. Re-add a `block: collection` with `view: citation` when ready.
---
