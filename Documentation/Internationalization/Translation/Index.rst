.. ==================================================
.. FOR YOUR INFORMATION
.. --------------------------------------------------
.. -*- coding: utf-8 -*- with BOM.

.. include:: ../../Includes.txt



.. _xliff-translating:

Translating XLIFF files
-----------------------

This sections highlights the different ways to translate XLIFF files.


.. _xliff-translating-server:

The TYPO3 translation server
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The TYPO3 community manages an official translation server, running
`Pootle <http://translate.sourceforge.net/wiki/pootle/index>`_. Localization files
in English are uploaded on that server and translations are packaged nightly.
They are fecthed in the TYPO3 CMS backend, via the Extension Manager (or the
new "Language" module since version 6.0).

It is not the point of this manual to go into the details of the translation
process. More information can be found in the `TYPO3 wiki <http://wiki.typo3.org/Translation>`_.


.. _xliff-translating-local:

Translating locally
^^^^^^^^^^^^^^^^^^^

Using `Virtaal <http://translate.sourceforge.net/wiki/virtaal/index>`_,
it is possible to translate XLIFF files locally.
Virtaal is an open source, cross-platform application.

.. figure:: ../../Images/XliffWithVirtaal.png
   :alt: Virtaal screenshot

   Translating with Virtaal, with suggestions from other software

Translating files locally is useful for extensions which are not meant to be
published or for creating :ref:`custom translations <xliff-translating-custom>`.


.. _xliff-translating-custom:

Custom translations
^^^^^^^^^^^^^^^^^^^

The :code:`$GLOBALS['TYPO3_CONF_VARS']['SYS']['locallangXMLOverride']` allows to
override both locallang-XML and XLIFF files. Actually this is not just about translations.
Default language files can also be overridden. In the case of XLIFF files, the
syntax is as follows::

   $GLOBALS['TYPO3_CONF_VARS']['SYS']['locallangXMLOverride']['path/to/originalTranslationFile.xlf'][] = 'path/to/otherTranslationFile.xlf';
   $GLOBALS['TYPO3_CONF_VARS']['SYS']['locallangXMLOverride']['fr']['path/to/originalTranslationFile.xlf'][] = 'other/path/to/fr.otherTranslationFile.xlf';

The first line shows how to override a file in the default language,
the second how to override a French ("fr") translation.


.. _xliff-translating-languages:

Custom languages
^^^^^^^^^^^^^^^^

Going further it is even possible - since TYPO3 CMS 4.6 - to add custom
languages to the TYPO3 backend and create the translations locally using
XLIFF files.

First of all, the language must be declared::

   $GLOBALS['TYPO3_CONF_VARS']['SYS']['localization']['locales']['user'] = array(
       'de_CH' => 'Swiss German',
   );

This new language does not need to be entirely translated. It can be defined
as falling back to another language, so that only differing labels need be
translated::

  $GLOBALS['TYPO3_CONF_VARS']['SYS']['localization']['locales']['dependencies'] = array(
     'de_CH' => array('de_AT', 'de'),
  );

In this case we define that "de_CH" can fall back on "de_AT" (another custom
translation) and then on "de".

The translations have to be stored in the appopriate folder, in this case
:file:`typo3conf/l10n/de_CH`.

The very least you need is to translate the label containing the name of the
language itself, so that it appears in the user preferences. In our example
this would be in file :file:`typo3conf/l10n/de_CH/setup/mod/de_CH.locallang.xlf`.

.. code:: xml

   <?xml version='1.0' encoding='utf-8'?>
   <xliff version="1.0">
      <file source-language="en" target-language="de_CH" datatype="plaintext" original="messages" product-name="setup">
         <header/>
         <body>
            <trans-unit id="lang_de_CH" approved="yes" xml:space="preserve">
               <source>Swiss German</source>
               <target state="translated">Swiizertütsch</target>
            </trans-unit>
         </body>
      </file>
   </xliff>

.. figure:: ../../Images/XliffCustomLanguage.png
   :alt: User Settings screenshot

   The new language appears in the user preferences
