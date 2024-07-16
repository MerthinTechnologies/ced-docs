# Link Contextual Help Slots with Intercom Articles

This tutorial will guide you through the process of linking Contextual Help Slots to use Intercom articles

## Prerequisites

Have an [Intercom](https://www.intercom.com/) account.

## Linking Process

1 - Go to the articles tab on Intercom and click on the article you desire to link
2 - Grab the seven-digit (typically) number from the url after the "articles" word. This is the 'articleId' property that we will use later
3 - Travel to [Contextual Help Slots](https://github.com/MerthinTechnologies/CloudEdgeDistribution/blob/master/spa/src/app/configuration/contextual-help-slots.ts)
4 - Find the name of the slot you desire to link to an article. For example, 'projects.list.empty-placeholder', then fill out the articleId with the number acquired before
5 - Change 'visible' property value to true. This will make a button appear in the component that will trigger Intercom and provide the article

## Troubleshooting

If Intercom launches, but it does not take you to the article. Go to Intercom and make sure the article is "Published" and not in "Drafted" under the status tab.
