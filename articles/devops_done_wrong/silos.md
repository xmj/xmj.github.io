Continuing Silos
================

Under traditional methodologies, waterfall and the likes, companies have
compartmentalized software development and platform operations into two
dedicated organizational units, often with entirely different management lines
imposed from the top.

This model can be continued by adding a third component into the mix - hiring
dedicated "DevOps staff" to sit in-between between developers and operators.

Companies need to satisfy stakeholder demands for state of the art in-house
knowledge on deployment software of the day, be it "configuration management"
or "infrastructure as code" software.

Popular with this model is to keep infrastructure changes within operations, so
that development teams "provide the software", and DevOps teams "provide the
infra glue" and operations "provide deployments".

What obtains is that people writing the software are twice-removed from its effects,
and that those who write the "infra glue" do not have their skin in the game
during deployments.

Combine that with on-call duties separated into yet another team (!) and you
can virtually guarantee hilarity ensuing left right and center.

Software developers work very differently when their sleep is put at risk.
DevOps staff will be much more diligent in ensuring everything is well tested
and stable before it touches integration environments.

What seems to work much less wrong: forming mixed teams involving all three
groups mentioned above, rotating on-call duties - and checklists.
